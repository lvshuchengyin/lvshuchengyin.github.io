title: flask wtf form template渲染
author: Lscy
tags:
  - python
categories:
  - 编程
date: 2018-05-20 10:49:00
---
flask wtf form template渲染
~~~ html
<form action="" method="POST" role="form" class="admin-form form-horizontal" enctype="multipart/form-data">
    {{ task_form.csrf_token }}
 
    {{ task_form.hidden_tag() }}
 
    {% for field, widget in task_form._fields.iteritems() %}
        {% if field != "csrf_token" %}
            <ul class="col-md-offset-2" style="color:red">
                {{ ', '.join(task_form.errors[field]) }}
            </ul>
 
            <div class="form-group">
                {{ task_form[field].label(class="col-md-2 control-label") }}
 
                <div class="col-md-10">
                    {{ task_form[field](class="form-control") }}
                </div>
            </div>
        {% endif %}
    {% endfor %}
 
    <div class="form-group">
        <div class="col-md-offset-2 col-md-10 submit-row">
            <input type="submit" class="btn btn-primary" value="保存">
        </div>
    </div>
 
</form>
~~~