title: 常用js代码
author: Lscy
tags:
  - js
categories:
  - 编程
date: 2018-05-20 10:14:00
---
### 判断是否ip地址
~~~ js
function check_is_ip(s) {
    var patt = /^(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])(\.(\d{1,2}|1\d\d|2[0-4]\d|25[0-5])){3}$/;
    return patt.test(s);
}
~~~

### 字符串格式化
~~~ js
String.prototype.format  = function() {    
    var args = arguments;    
    return this.replace(/\{(\d+)\}/g, function(m,i) {    
        return args[i];    
    });    
};
~~~
<!-- more -->

### 随机数
~~~ js
function getRandomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
~~~

### 打开新的tab
~~~ js
window.open('www.yourdomain.com','_blank');
~~~

### 重定向
~~~ js
window.location = "http://www.yourdomain.com";
~~~

### 清除字符串两边空格
~~~ js
s = $.trim(s)
~~~

### string转int
~~~ js
// parseInt(string, radix)
var x = parseInt("1000", 10);
// 如果转换的不是数字，则会返回NaN，可以用isNaN(x)来判断
// 缺点：并且如果转换的字符串是 123abc，则会返回123
 
// 使用正则来转换
function str2int(x) {
    if( /^\s*(\+|-)?\d+\s*$/.test(String(x)) ){
        return parseInt(x, 10);
    }
    return Number.NaN;
}
~~~

### ajax请求
~~~ js
$.ajax({
    type: 'POST',
    url: url,
    data: JSON.stringify(data),
    contentType: "application/json",  // 发送信息至服务器时内容编码类型
    beforeSend: function() {
        // 在发送请求之前调用，并且传入一个 XMLHttpRequest 作为参数。
    },
    success: function(data, textStatus, jqXHR) {
        // 当请求之后调用。传入返回后的数据，以及包含成功代码的字符串。
    },
    error: function(jqXHR, textStatus, errorThrown) { // if error occured
        // 在请求出错时调用。传入 XMLHttpRequest 对象，描述错误类型的字符串以及一个异常对象（如果有的话）
        alert(jqXHR.statusText + jqXHR.responseText);
    },
    complete: function(data|jqXHR, textStatus, jqXHR|errorThrown) {
        // 当请求完成之后调用这个函数，无论成功或失败。传入 XMLHttpRequest 对象，以及一个包含成功或错误代码的字符串。
    },
    dataType: 'json'，        //预期服务器返回的数据类型
});
~~~

### select
~~~ js
# 增加项
$('select.input-channel').append($('<option>', {
    value: "v",
    text: "t",
}));
 
# 监测变化
$("#select-time-range").change(function() {
    console.log('change');
});
~~~

### 交换两行
~~~ js
$("body").on("click", ".btn-index-down", function(){
    var trLength = $(".btn-index-down").length;
    var $tr = $(this).parent().parent();
    if ($tr.index() != trLength - 1) {
        $tr.next().after($tr);
    }
});
 
$("body").on("click", ".btn-index-up", function(){
    var $tr = $(this).parent().parent();
    if ($tr.index() != 0) {
        $tr.prev().before($tr);//在每个匹配的元素之前插入内容。
    }
});
~~~

### 动态生成的元素捕获事件
~~~ js
$("body").on("click", ".result-table-th", function() {
    //
});
~~~

### js 转移html字符
~~~ js
var entityMap = {
  '&': '&amp;',
  '<': '&lt;',
  '>': '&gt;',
  '"': '&quot;',
  "'": '&#39;',
  '/': '&#x2F;',
  '`': '&#x60;',
  '=': '&#x3D;'
};
 
function escapeHtml (string) {
  return String(string).replace(/[&<>"'`=\/]/g, function (s) {
    return entityMap[s];
  });
}
~~~

### 字体
~~~ css
"Helvetica Neue",Roboto,Arial,"Droid Sans",sans-serif
~~~