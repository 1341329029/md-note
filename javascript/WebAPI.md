# Web API

## Web API介绍

### API的概念

API（Application Programming Interface,应用程序编程接口）是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。

- 任何开发语言都有自己的API
- API的特征输入和输出(I/O)
- API的使用方法(console.log())

### Web API的概念

浏览器提供的一套操作浏览器功能和页面元素的API(BOM和DOM)

此处的Web API特指浏览器提供的API(一组方法)，Web API在后面的课程中有其它含义

### 掌握常见的浏览器提供的API的调用方式

[MDN-Web API](https://developer.mozilla.org/zh-CN/docs/Web/API)

### JavaScript的组成

![1496912475691](images/1496912475691.png)

#### ECMAScript - JavaScript的核心

定义了javascript的语法规范

JavaScript的核心，描述了语言的基本语法和数据类型，ECMAScript是一套标准，定义了一种语言的标准与具体实现无关

#### BOM - 浏览器对象模型

一套操作浏览器功能的API

通过BOM可以操作浏览器窗口，比如：弹出框、控制浏览器跳转、获取分辨率等

#### DOM - 文档对象模型

一套操作页面元素的API

DOM可以把HTML看做是文档树，通过DOM提供的API可以对树上的节点进行操作

## BOM

### BOM的概念

BOM(Browser Object Model) 是指浏览器对象模型，浏览器对象模型提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。BOM由多个对象组成，其中代表浏览器窗口的Window对象是BOM的顶层对象，其他对象都是该对象的子对象。

我们在浏览器中的一些操作都可以使用BOM的方式进行编程处理，

比如：刷新浏览器、后退、前进、在浏览器中输入URL等

### BOM的顶级对象window

window是浏览器的顶级对象，当调用window下的属性和方法时，可以省略window
注意：window下一个特殊的属性 window.name

## DOM

### DOM的概念

文档对象模型（Document Object Model，简称DOM），是[W3C](http://baike.baidu.com/item/W3C)组织推荐的处理可扩展标志语言的标准编程接口。在网页上，组织页面（或文档）的对象被组织在一个树形结构中，用来表示文档中对象的标准模型就称为DOM。Document Object Model的历史可以追溯至1990年代后期微软与[Netscape](http://baike.baidu.com/item/Netscape)的“浏览器大战”，双方为了在[JavaScript](http://baike.baidu.com/item/JavaScript)与[JScript](http://baike.baidu.com/item/JScript)一决生死，于是大规模的赋予浏览器强大的功能。微软在网页技术上加入了不少专属事物，既有[VBScript](http://baike.baidu.com/item/VBScript)、[ActiveX](http://baike.baidu.com/item/ActiveX)、以及微软自家的[DHTML](http://baike.baidu.com/item/DHTML)格式等，使不少网页使用非微软平台及浏览器无法正常显示。DOM即是当时蕴酿出来的杰作。

DOM又称为文档树模型

![1497154623955](media/1497154623955.png)

- 文档：一个网页可以称为文档
- 节点：网页中的所有内容都是节点（标签、属性、文本、注释等）
- 元素：网页中的标签
- 属性：标签的属性

### 模拟文档树结构

![1497165666684](media/1497165666684.png)

```javascript
function Element(option) {
  this.id = option.id || '';
  this.nodeName = option.nodeName || '';
  this.nodeValue = option.nodeValue || '';
  this.nodeType = 1;
  this.children = option.children || [];
}

var doc = new Element({
  nodeName: 'html'
});
var head = new Element({
  nodeName: 'head'
});
var body = new Element({
  nodeName: 'body'
})
doc.children.push(head);
doc.children.push(body);

var div = new Element({
  nodeName: 'div',
  nodeValue: 'haha',
});

var p = new Element({
  nodeName: 'p',
  nodeValue: '段落'
})
body.children.push(div);
body.children.push(p);

function getChildren(ele) {
  for(var i = 0; i < ele.children.length; i++) {
    var child = ele.children[i];
    console.log(child.nodeName);
    getChildren(child);
  }
}
getChildren(doc);
```

### DOM经常进行的操作

- 获取元素
- 动态创建元素
- 对元素进行操作(设置其属性或调用其方法)
- 事件(什么时机做相应的操作)

## 获取页面元素

### 为什么要获取页面元素

例如：我们想要操作页面上的某部分(显示/隐藏，动画)，需要先获取到该部分对应的元素，才进行后续操作

### 根据id获取元素

```javascript
var div = document.getElementById('main');
console.log(div);

// 获取到的数据类型 HTMLDivElement，对象都是有类型的
// HTMLDivElement <-- HTMLElement <-- Element  <-- Node  <-- EventTarget
```

注意：由于id名具有唯一性，部分浏览器支持直接使用id名访问元素，但不是标准方式，不推荐使用。

### 根据标签名获取元素

```javascript
var divs = document.getElementsByTagName('div');
for (var i = 0; i < divs.length; i++) {
  var div = divs[i];
  console.log(div);
}
```

### 根据name获取元素*

```javascript
var inputs = document.getElementsByName('hobby');
for (var i = 0; i < inputs.length; i++) {
  var input = inputs[i];
  console.log(input);
}
```

### 根据类名获取元素

```javascript
var mains = document.getElementsByClassName('main');
for (var i = 0; i < mains.length; i++) {
  var main = mains[i];
  console.log(main);
}
```

### 根据选择器获取元素

```javascript
var text = document.querySelector('#text');
console.log(text);

var boxes = document.querySelectorAll('.box');
for (var i = 0; i < boxes.length; i++) {
  var box = boxes[i];
  console.log(box);
}
```

- 总结

```
掌握
	getElementById()
	getElementsByTagName()
了解
	getElementsByName()
	getElementsByClassName()
	querySelector()
	querySelectorAll()
```

## 自定义属性

自定义属性不能通过直接通过DOM对象的方式来直接获取该属性的值

- getAttribute()获取自定义属性值

```javascript
<body>
<ul id="uu">
  <li score="10">助教的数学成绩</li>
  <li score="20">班主任的成绩</li>
  <li score="30">小苏的成绩</li>
  <li score="40">小杰老师成绩</li>
  <li score="50">乔峰成绩</li>
</ul>
<script src="common.js"></script>
<script>

  //html标签中有没有什么自带的属性可以存储成绩的----没有
  //本身html标签没有这个属性,自己(程序员)添加的,----自定义属性---为了存储一些数据

  //在html标签中添加的自定义属性,如果想要获取这个属性的值,需要使用getAttribute("自定义属性的名字")才能获取这个属性的值

  //获取所有的li标签
  var list=document.getElementsByTagName("li");
  for(var i=0;i<list.length;i++){
    list[i].onclick=function () {
        //alert(this.score);//不能
      //可以
      alert(this.getAttribute("score"));
    };
  }
</script>
</body>
```

- setAttribute()设置自定义属性值

```javascript
<body>
<ul id="uu">
  <li>助教的数学成绩</li>
  <li>班主任的成绩</li>
  <li>小苏的成绩</li>
  <li>小杰老师成绩</li>
  <li>乔峰成绩</li>
</ul>
<script src="common.js"></script>
<script>
   //获取所有的li标签,然后为每个标签中动态的添加自定义属性和值
  //点击的时候获取该标签的自定义属性的值

   //根据id获取ul标签,并且或者该标签中所有的li
  var list=my$("uu").getElementsByTagName("li");
  //循环遍历
  for(var i=0;i<list.length;i++){
    //先为每个li添加自定义属性
    //list[i].score=(i+1)*10;//此方式,自定义属性在DOM对象上,不在标签中
    list[i].setAttribute("score",(i+1)*10);
    //点击每个li标签,显示对应的自定义属性值
    list[i].onclick=function(){
      alert(this.getAttribute("score"));
    };
  }

</script>
</body>

```

- removeAttribute()移除自定义属性值

```javascript
<body>
<input type="button" value="移除自定义属性" id="btn"/>
<div id="dv" score="10" class="cls"></div>
<script src="common.js"></script>
<script>

  //移除自定义属性:removeAttribute("属性的名字")

  //点击按钮移除元素的自定义属性
  my$("btn").onclick=function () {
    //my$("dv").removeAttribute("score");
    //移除元素的类样式
    //值没有了,但是属性还是有的
    //my$("dv").className="";
    //也可以移除元素的自带的属性
    my$("dv").removeAttribute("class");
  };


</script>
```

### 自定义属性的操作

自定义属性:标签原本没有这个属性,为了存储数据,程序员自己添加的属性
自定义属性无法直接通过DOM对象的方式获取或者设置
对象.getAttribute("自定义属性名字");获取自定义属性的值
对象.setAttribute("属性名字","值");设置自定义属性及值
对象.removeAttribute("属性的名字");

### 总结

获取元素的方式

1. 根据id获取元素

>document.getElementyById("id属性的值");

2. 根据标签名字获取元素

>document.getElementysByTagName("标签的名字");

3. 根据name属性获取元素

>document.getElementysByName("name属性的值");

4. 根据类样式的名字获取元素

>document.getElementysByClassName("类样式的名字");

5. 根据选择器获取元素(返回一个对象)

>document.querySelector("选择器")

6. 根据选择器获取元素（返回数组，多个元素组成）

>document.querySelectorAll("选择器")

注： 3-6有的浏览器不支持

设置元素的样式的方式

- 对象.style.属性=值

- 对象。className=值

## 案例

1.点击按钮弹出对话框
2.点击按钮修改超链接的地址和热点文字
3.点击(每个)图片弹出对话框
4.点击图片设置自身宽和高
5.点击按钮修改每个图片的title属性
6.点击按钮显示哈哈(排他功能)
7.点击按钮显示和隐藏div
8.显示和隐藏二维码
9.点击按钮修改所有p标签内容
10.点击按钮修改所有文本框内容
11.点击按钮切换图片
12.点击超链接停止跳转页面
13.点击小图显示大图
14.美女相册
15点击按钮选中性别和兴趣

### innerText和textContent的兼容问题

目前的浏览器都支持innerText,应该是属于ie的标准
textContent本身是火狐支持,IE8不支持
innerText和innerHTML的区别
都可以设置标签的文本内容,如果要设置标签及内容推荐使用innerHTML
如果要获取标签中的文本,innerText,也可以使用innerHTML
如果想要获取的是有标签,也有文本---innerHTML

**兼容代码:**

```javascript
//设置任意元素的中间的文本内容
    function setInnnerText(element,text) {
      if(typeof element.textContent=="undefined"){
        element.innerText=text;
      }else{
        element.textContent=text;
      }
    }
    //获取任意元素的中间的文本内容
    function getInnerText(element) {
      if(typeof element.textContent=="undefined"){
       return element.innerText;
      }else{
       return element.textContent;
      }
    }
```

## 节点

文档:document
元素:页面中所有的标签,元素---element,  标签----元素---对象
节点:页面中所有的内容(标签,属性,文本(文字,换行,空格,回车)),Node
根元素:html标签

节点的属性:(可以使用标签--元素.出来,可以使用属性节点.出来,文本节点.点出来)

- nodeType:节点的类型:1----标签,2---属性,3---文本

- nodeName:节点的名字:标签节点---大写的标签名字,属性节点---小写的属性名字,文本节点----#text

- nodeValue:节点的值:标签节点---null,属性节点---属性值,文本节点---文本内容

### 获取节点和元素

```javascript
//12行代码:都是获取节点和元素的
  //ul
  var ulObj=document.getElementById("uu");
  //父级节点
  console.log(ulObj.parentNode);
  //父级元素
  console.log(ulObj.parentElement);
  //子节点
  console.log(ulObj.childNodes);
  //子元素
  console.log(ulObj.children);
  console.log("==============================================");
  //第一个子节点
  console.log(ulObj.firstChild);//------------------------IE8中是第一个子元素
  //第一个子元素
  console.log(ulObj.firstElementChild);//-----------------IE8中不支持
  //最后一个子节点
  console.log(ulObj.lastChild);//------------------------IE8中是第一个子元素
  //最后一个子元素
  console.log(ulObj.lastElementChild);//-----------------IE8中不支持
  //某个元素的前一个兄弟节点
  console.log(my$("three").previousSibling);
  //某个元素的前一个兄弟元素
  console.log(my$("three").previousElementSibling);
  //某个元素的后一个兄弟节点
  console.log(my$("three").nextSibling);
  //某个元素的后一个兄弟元素
  console.log(my$("three").nextElementSibling);
```

**注:** 凡是获取节点的代码在谷歌和火狐得到的都是  相关的节点
凡是获取元素的代码在谷歌和火狐得到的都是   相关的元素
从子节点和兄弟节点开始,凡是获取节点的代码在IE8中得到的是元素,获取元素的相关代码,在IE8中得到的是undefined----元素的代码,iE中不支持
19