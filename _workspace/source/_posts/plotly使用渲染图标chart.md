title: plotly使用渲染图标chart
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 11:33:00
---
### 使用bottle
~~~ python
import json
 
from bottle import route, run, template, Bottle, response
 
import argparse
import pandas as pd
 
from plotly import utils
import plotly.graph_objs as go
 
from requests.compat import json as _json
 
from influxdb import DataFrameClient
 
app = Bottle()
 
@app.hook('after_request')
def enable_cors():
    response.headers['Access-Control-Allow-Origin'] = '*'
    response.headers['Access-Control-Allow-Methods'] = 'GET, POST, PUT, OPTIONS'
    response.headers['Access-Control-Allow-Headers'] = 'Origin, Accept, Content-Type, X-Requested-With, X-CSRF-Token'
 
@app.route('/data')
def index():
    client = DataFrameClient('127.0.0.1', '8086', database='dc')
    res = client.query('select sum(succ), sum(fail) from p group by host limit 10')
 
    data = []
    for metric, df in res.items():
        print df
        trace = go.Bar(
            x=df[df.columns[0]],
            y=df[df.columns[1]],
            name=str(metric),
        )
        data.append(trace)
    layout = go.Layout()
    data_json = _json.dumps(data, cls=utils.PlotlyJSONEncoder)
    layout_json = _json.dumps(layout, cls=utils.PlotlyJSONEncoder)
    data_dict = json.loads(data_json)
    layout_dict = json.loads(layout_json)
    return {'records': data_dict, 'layout': layout_dict}
 
@app.route('/pie')
def pie():
    client = DataFrameClient('127.0.0.1', '8086', database='dc')
    res = client.query('select sum(succ), sum(fail) from p group by host limit 10')
 
    data = []
    labels = []
    pds = []
    for metric, df in res.items():
        print metric, df
        print '---------', df.columns, df.columns.values
        labels.append(str(metric) + df.columns[0])
        labels.append(str(metric) + df.columns[1])
        pds.append(df[df.columns[0]])
        pds.append(df[df.columns[1]])
    trace = go.Pie(
        labels=labels,
        values=pd.concat(pds),
        name=str(metric),
    )
    data.append(trace)
    layout = go.Layout()
    data_json = _json.dumps(data, cls=utils.PlotlyJSONEncoder)
    layout_json = _json.dumps(layout, cls=utils.PlotlyJSONEncoder)
    data_dict = json.loads(data_json)
    layout_dict = json.loads(layout_json)
    return {'records': data_dict, 'layout': layout_dict}
 
@app.route('/line')
def line():
    client = DataFrameClient('127.0.0.1', '8086', database='dc')
    res = client.query('select sum(succ), sum(fail) from p where time > now() - 1d and succ > 0 group by time(1h) limit 10')
 
    data = []
    for metric, df in res.items():
        print metric, df
        print '---------', df.index
        for col in df.columns.values:
            trace = go.Scatter(
                x=df.index,
                y=df[col],
                name=str(metric),
            )
            data.append(trace)
    layout = go.Layout()
    data_json = _json.dumps(data, cls=utils.PlotlyJSONEncoder)
    layout_json = _json.dumps(layout, cls=utils.PlotlyJSONEncoder)
    data_dict = json.loads(data_json)
    layout_dict = json.loads(layout_json)
    return {'records': data_dict, 'layout': layout_dict}
 
run(app, host='localhost', port=8080, debug=True)
~~~

### html
~~~ html
<html>
<head>
    <script src="http://code.jquery.com/jquery-3.2.1.min.js"></script>
    <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
</head>
 
<div id="plot" style="width:90%;height:600px;"></div>
<div id="plot_query"></div>
 
<script>
    function makeplot() {
        $.ajax({
            url: 'http://127.0.0.1:8080/pie',
            data: {
            },
            dataType: 'json',
            success: function (result) {
                console.log(result);
                //result = JSON.parse(result);
                console.log(result.records);
                console.log(result.layout);
                makePlotly(result.query, result.records, result.layout);
                document.getElementById("plot_query").innerHTML = result.query;
            }
        });
    };
 
    function makePlotly(title,  traces, layout){
        var plotDiv = document.getElementById("plot");
        Plotly.newPlot('plot', traces, layout);
    };
 
    makeplot();
</script>
</html>
~~~