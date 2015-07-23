<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [节点操作](#%E8%8A%82%E7%82%B9%E6%93%8D%E4%BD%9C)
    - [获取节点](#%E8%8E%B7%E5%8F%96%E8%8A%82%E7%82%B9)
      - [通过节点/元素属性获取](#%E9%80%9A%E8%BF%87%E8%8A%82%E7%82%B9%E5%85%83%E7%B4%A0%E5%B1%9E%E6%80%A7%E8%8E%B7%E5%8F%96)
        - [节点遍历](#%E8%8A%82%E7%82%B9%E9%81%8D%E5%8E%86)
        - [元素遍历](#%E5%85%83%E7%B4%A0%E9%81%8D%E5%8E%86)
- [h1](#h1)
      - [通过接口获取节点（推荐）](#%E9%80%9A%E8%BF%87%E6%8E%A5%E5%8F%A3%E8%8E%B7%E5%8F%96%E8%8A%82%E7%82%B9%EF%BC%88%E6%8E%A8%E8%8D%90%EF%BC%89)
        - [getElementById](#getelementbyid)
        - [getElementsByTagName](#getelementsbytagname)
        - [getElementsByClassName](#getelementsbyclassname)
        - [querySelector](#queryselector)
        - [querySelectorAll](#queryselectorall)
        - [各接口比较](#%E5%90%84%E6%8E%A5%E5%8F%A3%E6%AF%94%E8%BE%83)
  - [8882 People is learning this lesson.](#8882-people-is-learning-this-lesson)
  - [8882 People is learning this lesson.](#8882-people-is-learning-this-lesson-1)
  - [8882 People is learning this lesson.](#8882-people-is-learning-this-lesson-2)
  - [8882 People is learning this lesson.](#8882-people-is-learning-this-lesson-3)
  - [8882 People is learning this lesson.](#8882-people-is-learning-this-lesson-4)
    - [创建节点](#%E5%88%9B%E5%BB%BA%E8%8A%82%E7%82%B9)
    - [修改节点](#%E4%BF%AE%E6%94%B9%E8%8A%82%E7%82%B9)
      - [通过 textContent 修改节点](#%E9%80%9A%E8%BF%87-textcontent-%E4%BF%AE%E6%94%B9%E8%8A%82%E7%82%B9)
      - [通过 innerText 修改节点 （不符合 W3C 规范）](#%E9%80%9A%E8%BF%87-innertext-%E4%BF%AE%E6%94%B9%E8%8A%82%E7%82%B9-%EF%BC%88%E4%B8%8D%E7%AC%A6%E5%90%88-w3c-%E8%A7%84%E8%8C%83%EF%BC%89)
    - [插入节点](#%E6%8F%92%E5%85%A5%E8%8A%82%E7%82%B9)
      - [通过 appendChild 插入](#%E9%80%9A%E8%BF%87-appendchild-%E6%8F%92%E5%85%A5)
      - [通过 insertBefore 插入](#%E9%80%9A%E8%BF%87-insertbefore-%E6%8F%92%E5%85%A5)
    - [删除节点](#%E5%88%A0%E9%99%A4%E8%8A%82%E7%82%B9)
    - [innerHTML](#innerhtml)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 节点操作

### 获取节点

#### 通过节点/元素属性获取

##### 节点遍历

- node.parentNode 		父节点
- node.childNodes		所有子节点
- node.previousSibling 前一个兄弟节点
- node.nextSibling		后一个兄弟节点
- node.firstChild		第一个子节点
- node.lastChild		最后一个子节点	

```Javascript 
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body><ul id="ul"><li>First</li><li>Second</li><li>Third</li><li>Fourth</li></ul><p>Hello</p>
	<script type="text/javascript">
		var ulNode = document.getElementsByTagName("ul")[0]; 
		console.log(ulNode.parentNode);		//<body></body>
		console.log(ulNode.previousSibling);	//null
		console.log(ulNode.nextSibling);	//<p>Hello</p>
		console.log(ulNode.firstChild);	//<li>First</li>
		console.log(ulNode.lastChild);	//<li>Fourth</li>
	</script>
</body>
</html>
```

##### 元素遍历

- node.children	 获取所有的子元素
- element.previousElementSibling 获取前一个兄弟元素
- element.nextElementSibling	获取后一个兄弟元素
- element.firstElementChild		获取第一个子元素
- element.lastElementChild		获取最后一个子元素

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<ul id="ul">
		<li>First</li>
		<li>Second</li>
		<li>Third</li>
		<li>Fourth</li>
	</ul>
	<p>Hello</p>
	<script type="text/javascript">
		var ulNode = document.getElementsByTagName("ul")[0]; 
		console.log(ulNode.parentNode);		//<body></body>
		console.log(ulNode.previousElementSibling);	//null
		console.log(ulNode.nextElementSibling);	//<p>Hello</p>
		console.log(ulNode.firstElementChild);	//<li>First</li>
		console.log(ulNode.lastElementChild);	//<li>Fourth</li>
	</script>
</body>
</html>
```

***NTOE：细心地人会发现，在节点遍历的例子中，body、ul、li、p节点之间是没有空格的，因为如果有空格，那么空格就会被当做一个TEXT节点，从而用ulNode.previousSibling获取到得就是一个空的文本节点，而不是`<li>First</li>`节点了。即节点遍历的几个属性会得到所有的节点类型，而元素遍历只会得到相对应的元素节点。一般情况下，用得比较多的还是元素节点的遍历属性。***

**实现浏览器兼容版的element.children**

有一些低版本的浏览器并不支持element.children方法，但我们可以用下面的方式来实现兼容。

```html
<html lang>
<head>
	<meta charest="utf-8">
	<title>Compatible Children Method</title>
</head>
<body id="body">
	<div id="item">
		<div>123</div>
		<p>ppp</p>
		<h1>h1</h1>
	</div>
	<script type="text/javascript">
		function getElementChildren(e){
			if(e.children){
				return e.children;
			}else{
				/* compatible other browse */
				var i, len, children = [];
				var child = element.firstChild;
				if(child != element.lastChild){
					while(child != null){
						if(child.nodeType == 1){
							children.push(child);
						}
						child = child.nextSibling;
					}
				}else{
					children.push(child);
				}
				return children;
			}
		}
		/* Test method getElementChildren(e) */
		var item = document.getElementById("item");
		var children = getElementChildren(item);
		for(var i =0; i < children.length; i++){
			alert(children[i]);
		}
	</script>
</body>
</html>
```
NOTE：初稿，还未进行兼容性测试。

#### 通过接口获取节点（推荐）

- `getElementById`
- `getElementsByTagName`
- `getElementsByClassName`
- `querySelector`
- `querySelectorAll`

##### getElementById

获取文档中指定 `id` 的节点**对象**。

- 返回一个元素节点

- 必须作用于document对象上

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<ul id="ul">ddd
		<li>First</li>
		<li>Second</li>
		<li>Third</li>
		<li>Fourth</li>
	</ul>
	<p>Hello</p>
	<script type="text/javascript">
		var ulNode = document.getElementById("ul"); //<ul></ul>
	</script>
</body>
</html>
```

##### getElementsByTagName

动态的获取具有指定标签元素节点的集合

- 返回一个集合

- 不必直接作用于 `document` 之上，可直接通过元素而获取

- 其返回值**会**被 DOM 的变化所影响，值会发生变化

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<ul id="ul">ddd
		<li>First</li>
		<li>Second</li>
		<li>Third</li>
		<li>Fourth</li>
	</ul>
	<p>Hello</p>
	<script type="text/javascript">
		var liNodes = document.getElementsByTagName("li"); // li*4
		alert("Make a breakpoint here to see the liNodes value");
	</script>
</body>
</html>
```

##### getElementsByClassName

获取所有有指定class名的元素，多个class可用空格隔开

- 返回一个集合

- 不必直接作用于 `document` 之上，可直接通过元素而获取

- 其返回值**会**被 DOM 的变化所影响，值会发生变化

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<ul id="ul">ddd
		<li class="red">First</li>
		<li class="red">Second</li>
		<li class="red">Third</li>
		<li class="red transparent">Fourth</li>
	</ul>
	<p>Hello</p>
	<script type="text/javascript">
		var ulNode = document.getElementById("ul");
		var liNodes = ulNode.getElementsByClassName("red"); // <li>First</li><li>Second</li><li>Third</li><li>Fourth</li>
		var fourthNode = ulNode.getElementsByClassName("red transparent"); //<li>Fourth</li>
		alert("Make a breakpoint here to see the liNodes value");
	</script>
</body>
</html>
```

NOTE：IE9 以下版本不支持 `getElementsByClassName`

**兼容方法**

```javascript
function getElementsByClassName(root, className) {
  // 特性侦测
  if (root.getElementsByClassName) {
    // 优先使用 W3C 规范接口
    return root.getElementsByClassName(className);
  } else {
    // 获取所有后代节点
    var elements = root.getElementsByTagName('*');
    var result = [];
    var element = null;
    var classNameStr = null;
    var flag = null;

    className = className.split(' ');

    // 选择包含 class 的元素
    for (var i = 0, element; element = elements[i]; i++) {
      classNameStr = ' ' + element.getAttribute('class') + ' ';
      flag = true;
      for (var j = 0, name; name = className[j]; j++) {
        if (classNameStr.indexOf(' ' + name + ' ') === -1) {
          flag = false;
          break;
        }
      }
      if (flag) {
        result.push(element);
      }
    }
    return result;
  }
}
```

##### querySelector

`element.querySelector(selector)`

获取符合选择器的单个元素。如果有多个元素符合条件，则取第一个。

- 返回一个元素节点

- 不必直接作用于 `document` 之上，可直接通过元素而获取

- 其返回值**不会**被 DOM 的变化所影响，值不会发生变化

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<ul id="ul">
		<li id="first" class="red">First</li>
		<li id="second" class="red">Second</li>
		<li id="third" class="red">Third</li>
		<li id="fourth" class="red transparent">Fourth</li>
	</ul>
	<p>Hello</p>
	<script type="text/javascript">
		var ulNode = document.getElementById("ul");
		var firstNode = ulNode.querySelector(".red"); //<li>First</li>
		var secondNode = ulNode.querySelector("#second"); //<li>Second</li>
		var fourthNode = ulNode.querySelector("#fourth.red.transparent"); //<li>Fourth</li>
		alert("Make a breakpoint here to see the liNodes value");
	</script>
</body>
</html>
```

NOTE: IE9 一下不支持 `querySelector` 与 `querySelectorAll`（写一个兼容的方法）

##### querySelectorAll

`element.querySelectorAll(selector)`

获取符合选择器的多个元素。

- 返回一个集合

- 不必直接作用于 `document` 之上，可直接通过元素而获取

- 其返回值**不会**被 DOM 的变化所影响，值不会发生变化

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<ul id="ul">
		<li id="first" class="red">First</li>
		<li id="second" class="red">Second</li>
		<li id="third" class="red">Third</li>
		<li id="fourth" class="red transparent">Fourth</li>
	</ul>
	<p>Hello</p>
	<script type="text/javascript">
		var ulNode = document.getElementById("ul");
		var redLis = ulNode.querySelectorAll(".red");
		alert("Make a breakpoint here to see the liNodes value");
	</script>
</body>
</html>
```

##### 各接口比较

|API|只作用于 `document`|唯一返回值|live|
|---|:-----------------:|:--------:|:--:|
|getElementById|√|√||
|getElementsByTagName|||√|
|getElementsByClassName|||√|
|querySelectorAll||||
|querySelector||√||

- getElementsByTagName、queryElementsByClassName 获取的节点会随着DOM节点的改变而改变

- getElementById、querySelector、querySelectorAll 获取的节点是固定的，不会随着DOM节点的改变而改变。

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Test</title>
</head>
<body>
<div id="users">
	<h2>8882 People is learning this lesson.</h2>
	<ul>
		<li class="user">Satoshi</li>
		<li class="user">Spring</li>
		<li id="lastUser" class="user last">Kash</li>
	</ul>
</div>
<script type="text/javascript">
	var users = document.getElementById("users");
	/* getElementsByTagName  会随之改变*/
	// var userList = users.getElementsByTagName("li");
	// alert(userList.length + "个用户"); 

	/* getElementsByClassName 会随之改变*/
	// var userList = users.getElementsByClassName("user");
	// alert(userList.length + "个用户"); 

	/* querySelectorAll 不会随之改变*/
	var userList = users.querySelectorAll(".user");
	alert(userList.length + "个用户"); 	

	/* 去掉一个子元素  */
	var lastUser = document.getElementById("lastUser");
	lastUser.parentNode.removeChild(lastUser);
	alert(userList.length + "个用户");
</script>
</body>
</html>
```

### 创建节点

`var tagNameElement = document.createElement('tagName');`

创建一个元素节点

`var textElement = document.createTextNode('tagName');`

创建一个文本节点

```html
var bodyNode = document.getElementsByTagName("body")[0]; //Get the <body> node
var pNode = document.createElement("p");	//create a new <p> node
var txtNode = document.createTextNode("Here is the text content"); //create a new text node
divNode.appendChild(txtNode);
bodyNode.appendChild(divNode);
```

### 修改节点

#### 通过 textContent 修改节点

获取或设置**节点以及其后代节点**的文本内容

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<div id="users">
		<h2>8882 People is learning this lesson.</h2>
		<ul>
			<li class="user">Satoshi</li>
			<li class="user">c</li>
			<li id="lastUser" class="user last">Kash</li>
		</ul>
	</div>
	<script type="text/javascript">
		var users = document.getElementById("users");
		/*  1. conetnt = "8882 People is learning this lesson. Satoshi Satoshi Kash" */
		var content = users.textContent; 
		/*  2. 设置user_last元素的文本内容为"Tom" */
		var user_last = document.getElementById("lastUser");
		user_last.textContent = "Tom";
	</script>
</body>
</html>
```

NOTE：不支持 IE 9 及以下版本不支持 textContent。

#### 通过 innerText 修改节点 （不符合 W3C 规范）

获取或设置**节点以及其后代节点**的文本内容

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<div id="users">
		<h2>8882 People is learning this lesson.</h2>
		<ul>
			<li class="user">Satoshi</li>
			<li class="user">c</li>
			<li id="lastUser" class="user last">Kash</li>
		</ul>
	</div>
	<script type="text/javascript">
		var users = document.getElementById("users");
		/*  1. conetnt = "8882 People is learning this lesson. Satoshi Satoshi Kash" */
		var content = users.innerText; 
		/*  2. 设置user_last元素的文本内容为"Tom" */
		var user_last = document.getElementById("lastUser");
		user_last.innerText = "Tom";
	</script>
</body>
</html>
```

**innerText 不符合 W3C 规范**，但我们却经常使用这种方式去设置元素的文本值。innerText还有一个问题，即它不支持 FireFox 浏览器。但我们可以通过下面的方面来兼容

**FireFox 兼容方案**

```javascript
if (!('innerText' in document.body)) { //特性检测
  HTMLElement.prototype.__defineGetter__('innerText', function(){
    return this.textContent;
  });
  HTMLElement.prototype.__defineSetter__('innerText', function(s) {
    return this.textContent = s;
  });
}
```

### 插入节点

#### 通过 appendChild 插入

`parentNode.appendChild(childNode)`

在parentNode里加入childNode，默认插入到子元素末尾

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<div id="users">
		<h2>8882 People is learning this lesson.</h2>
		<ul id="ul">
			<li class="user">Satoshi</li>
			<li class="user">c</li>
			<li id="lastUser" class="user last">Kash</li>
		</ul>
	</div>
	<script type="text/javascript">
		var ulNode = document.getElementById("ul");
		/* 创建li节点 */
		var liNode = document.createElement("li");
		var liTextNode = document.createTextNode("ChanShuYi");
		liNode.appendChild(liTextNode);
		/* 增加li节点到ul节点中 */
		ulNode.appendChild(liNode);
	</script>
</body>
</html>
```

#### 通过 insertBefore 插入

`var aChild = parentNode.insertBefore(childNode, referenceNode)`

在element元素里插入childNode元素，并且是在referenceNode元素前插入

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>ELEMENT_NODE & TEXT_NODE</title>
</head>
<body>
	<div id="users">
		<h2>8882 People is learning this lesson.</h2>
		<ul id="ul">
			<li class="user">Satoshi</li>
			<li class="user">c</li>
			<li id="lastUser" class="user last">Kash</li>
		</ul>
	</div>
	<script type="text/javascript">
		var ulNode = document.getElementById("ul");
		/* 创建li节点 */
		var liNode = document.createElement("li");
		var liTextNode = document.createTextNode("ChanShuYi");
		liNode.appendChild(liTextNode);
		/* 获取参考点 */
		var lastUserNode = document.getElementById("lastUser");
		/* 增加li节点到ul节点中 */
		ulNode.insertBefore(liNode, lastUserNode);
	</script>
</body>
</html>
```

### 删除节点

`var parentNode = element.removeChild(childNode)`

删除指定节点的子元素节点

### innerHTML

获取或设置指定节点之中所有的 HTML 内容。   

- `innerHTML` 不检查内容，直接运行创建一批全新的节点

- 之前节点设置和绑定的事件和样式都会消失

NOTE：只建议在创建全新的节点时使用。不可在用户可控的情况下使用。

```javascript
var elementsHTML = element.innerHTML;
element.innerHTML = "<a href='www.cnblogs.com/chanshuyi'>点击跳转博客</a>";
```

**存在的问题** 

- 低版本 IE 存在内存泄露
- 安全问题（用户可以在名称中运行脚本代码）