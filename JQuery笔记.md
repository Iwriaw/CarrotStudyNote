# JQuery 学习笔记
## 选择器
### 元素选择器
选取所有\<p>元素：
```js
$("p")
```
### #id选择器
选取所有id为test的元素：
```js
$("#test")
```
### .类选择器
选取所有class为test的元素：
```js
$(".test")
```
## 事件
页面对不同访问者的响应叫做事件。

事件处理程序指的是当 HTML 中发生某些事件时所调用的方法。

### 常见 DOM 事件：

| 鼠标事件         | 键盘事件       | 表单事件        | 文档/窗口事件    |
| ---------------- | -------------- | --------------- | ---------------- |
| click(点击)      | keypress(按键) | submit(提交)    | load(加载)       |
| dblclick(双击)   | keydown(按下)  | change(改变)    | resize(改变大小) |
| mouseenter(进入) | keyup(抬起)    | focus(获得焦点) | scroll(滚动)     |
| mouseleave(离开) |                | blur(失去焦点)  | unload(卸载)     |
| hover(进入,离开) |                |                 |                  |

### 事件方法语法
在页面中指定一个点击事件：
```js
$("p").click();
```
定义点击后的触发事件：
```js
$("p").click(function(){
    // 动作触发后执行的代码!!
});
```
## 捕获和设置
jQuery 中非常重要的部分，就是操作 DOM 的能力。

jQuery 提供一系列与 DOM 相关的方法，这使访问和操作元素和属性变得很容易。

### text()
设置或返回所选元素的文本内容
```js
$("#btn1").click(function(){
    $("#test1").text("Hello world!");
});
```
```js
$("#btn1").click(function(){
  alert("Text: " + $("#test").text());
});
```
### html()
设置或返回所选元素的内容（包括 HTML 标记）
```js
$("#btn2").click(function(){
    $("#test2").html("<b>Hello world!</b>");
});
```
```js
$("#btn2").click(function(){
  alert("HTML: " + $("#test").html());
});
```
### val()
设置或返回表单字段的值
```js
$("#btn3").click(function(){
    $("#test3").val("RUNOOB");
});
```
```js
$("#btn1").click(function(){
  alert("值为: " + $("#test").val());
});
```#
### attr()
设置或返回所选元素的属性
```js
$("button").click(function(){
  $("#runoob").attr("href","http://www.runoob.com/jquery");
});
$("button").click(function(){
    $("#runoob").attr({
        "href" : "http://www.runoob.com/jquery",
        "title" : "jQuery 教程"
    });
});
```
```js
$("button").click(function(){
  alert($("#runoob").attr("href"));
});
```
## 添加删除元素
### append()
在被选元素的结尾插入内容
```js
$("p").append("追加文本");
//插入多个元素
function appendText(){
    var txt1="<p>文本-1。</p>";              // 使用 HTML 标签创建文本
    var txt2=$("<p></p>").text("文本-2。");  // 使用 jQuery 创建文本
    var txt3=document.createElement("p");
    txt3.innerHTML="文本-3。";               // 使用 DOM 创建文本 text with DOM
    $("body").append(txt1,txt2,txt3);        // 追加新元素
}
```
### prepend()
在被选元素的结尾开头内容
```js
$("p").prepend("在开头追加文本");
//插入多个元素
function prependText(){
    var txt1="<p>文本-1。</p>";              // 使用 HTML 标签创建文本
    var txt2=$("<p></p>").text("文本-2。");  // 使用 jQuery 创建文本
    var txt3=document.createElement("p");
    txt3.innerHTML="文本-3。";               // 使用 DOM 创建文本 text with DOM
    $("body").prepend(txt1,txt2,txt3);        // 追加新元素到开头
}
```
### after()
在被选元素之后插入内容
```js
$("img").after("在后面添加文本");
//插入多个元素
function afterText()
{
    var txt1="<b>I </b>";                    // 使用 HTML 创建元素
    var txt2=$("<i></i>").text("love ");     // 使用 jQuery 创建元素
    var txt3=document.createElement("big");  // 使用 DOM 创建元素
    txt3.innerHTML="jQuery!";
    $("img").after(txt1,txt2,txt3);          // 在图片后添加文本
}
```
### before()
在被选元素之前插入内容
```js
$("img").before("在前面添加文本");
//插入多个元素
function beforeText()
{
    var txt1="<b>I </b>";                    // 使用 HTML 创建元素
    var txt2=$("<i></i>").text("love ");     // 使用 jQuery 创建元素
    var txt3=document.createElement("big");  // 使用 DOM 创建元素
    txt3.innerHTML="jQuery!";
    $("img").before(txt1,txt2,txt3);          // 在图片前添加文本
}
```

### remove()
删除被选元素（及其子元素）
```js
$("#div1").remove();
//也可接受参数进行过滤
$("p").remove(".italic");
```
### empty()
从被选元素中删除子元素
```js
$("#div1").empty();
```
## 操作CSS
### addclass()
向被选元素添加一个或多个类
```js
//多个类之间用空格分隔
$("button").click(function(){
  $("body div:first").addClass("important blue");
});
```
### removeClass()
从被选元素删除一个或多个类
```js
//多个类之间用空格分隔
$("button").click(function(){
  $("h1,h2,p").removeClass("blue");
});
```
### toggleClass()
对被选元素进行添加/删除类的切换操作(没有就加，有就删除)
```js
//多个类之间用空格分隔
$("button").click(function(){
  $("h1,h2,p").toggleClass("blue");
});
```
### css()
设置或返回被选元素的一个或多个样式属性。
```js
//为所有匹配元素设置 background-color 值：
$("p").css("background-color","yellow");
//为所有匹配元素同时设置多个CSS属性
$("p").css({"background-color":"yellow","font-size":"200%"});
```
```js
//返回首个匹配元素的background-color值
$("p").css("background-color");
```

## 尺寸
### width()
width() 方法设置或返回元素的宽度（不包括内边距、边框或外边距）
### height()
height() 方法设置或返回元素的高度（不包括内边距、边框或外边距）。
### innerWidth()
innerWidth() 方法返回元素的宽度（包括内边距）。
### innerHeight()
innerHeight() 方法返回元素的高度（包括内边距）。
### outerWidth()
outerWidth() 方法返回元素的宽度（包括内边距和边框）。
### outerHeight()
outerHeight() 方法返回元素的高度（包括内边距和边框）。

## 遍历
### parent()
返回被选元素的直接父元素。
### parents()
返回被选元素的所有祖先元素，它一路向上直到文档的根元素 (<html>)。
### parentsUntil()
返回介于两个给定元素之间的所有祖先元素。
### children()
返回被选元素的所有直接子元素。
### find()
返回被选元素的后代元素。
### siblings()
返回被选元素的所有同胞元素。
### next()
返回被选元素的下一个同胞元素。
### prev()
返回被选元素的上一个同胞元素。
### nextAll()
返回被选元素的所有跟随的同胞元素。
### prevAll()
返回被选元素的所有之前的的同胞元素。
### nextUntil()
返回介于两个给定参数之间的所有跟随的同胞元素。
### prevUntil
返回介于两个给定参数之间的所有跟随的同胞元素。