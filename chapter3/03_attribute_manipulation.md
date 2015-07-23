<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [属性操作](#%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C)
  - [HTML 属性与 DOM 属性的对应](#html-%E5%B1%9E%E6%80%A7%E4%B8%8E-dom-%E5%B1%9E%E6%80%A7%E7%9A%84%E5%AF%B9%E5%BA%94)
  - [属性操作方式](#%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C%E6%96%B9%E5%BC%8F)
    - [通过属性访问器访问（Property Accessor）](#%E9%80%9A%E8%BF%87%E5%B1%9E%E6%80%A7%E8%AE%BF%E9%97%AE%E5%99%A8%E8%AE%BF%E9%97%AE%EF%BC%88property-accessor%EF%BC%89)
    - [通过 getAttribute/setAttribute 方法访问](#%E9%80%9A%E8%BF%87-getattributesetattribute-%E6%96%B9%E6%B3%95%E8%AE%BF%E9%97%AE)
  - [dataset 来存储数据](#dataset-%E6%9D%A5%E5%AD%98%E5%82%A8%E6%95%B0%E6%8D%AE)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 属性操作

### HTML 属性与 DOM 属性的对应

每个 HTML 属性都会对应相应的 DOM 对象属性。如下面代码中，ulNode对象的id属性就对应了html代码中ul元素的id属性。

```html
<html>
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
	<ul id="ul" class="non-decoration">
		<li>First</li>
		<li>Second</li>
		<li>Third</li>
		<li>Fourth</li>
	</ul>
	<p>Hello</p>
<script type="text/javascript">
	var ulNode = document.getElementById("ul");
	var ulId = ulNode.id;	//ul
	var ulType = ulNode.type;	//为空，因为ulNode没有type属性
	var ulClassName = ulNode.className; //non-decoration
	alert("Make a breakpoint here to see the liNodes value");
</script>
</body>
</html>
```

### 属性操作方式

#### 通过属性访问器访问（Property Accessor）

通过属性访问器得到的属性为转换过的实例对象（并非全字符串）。

**读取属性**

```html
<html>
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
	<select name="hobby" id="hobby" disabled>
		<option value="1">Basketball</option>
		<option value="2">Tennis</option>
		<option value="3">Football</option>
	</select>
<script type="text/javascript">
	var selectNode = document.getElementById("hobby");
	var isSelectDisabled = selectNode.disabled;	//boolean类型, true
	// alert(typeof(isSelectDisabled) == "boolean");	//true
	var selectId = selectNode.id;	//String类型，"hobby"
	// alert(typeof(selectId) == "string");	//true
	alert("Make a breakpoint here to see the liNodes value");
</script>
</body>
</html>
```

**写入属性**

可增加新的属性或改写已有属性。

```html
<html>
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
	<select name="hobby" id="hobby">
		<option value="1">Basketball</option>
		<option value="2">Tennis</option>
		<option value="3">Football</option>
	</select>
<script type="text/javascript">
	var optionNodes = document.querySelectorAll("#hobby option");
	/* 修改已有属性 */
	optionNodes[0].value = "Basketball";
	optionNodes[1].value = "Tennis";
	optionNodes[2].value = "Football";
	/* 增加新的属性 */
	optionNodes[0].className = "Basketball";
	optionNodes[1].className = "Tennis";
	optionNodes[2].className = "Football";
</script>
</body>
</html>
```

NOTE：为元素增加新的属性时，如果该属性不存在，那么设置是无效的。另外，通过`[]`来访问和通过`.`来访问设置属性是相同的，下面代码的效果是等值的：

```html
var value1 = optionNodes[0].className;
var value2 = optionNodes[0]["className"];
optionNodes[0].className = "Basketball";
optionNodes[0]["className"] = "Basketball";
```

**特点** 

- X 通用行差（命名异常，使用不同的命名方式进行访问）
- X 扩展性差
- √ 实用对象（取出后可直接使用）


#### 通过 getAttribute/setAttribute 方法访问

**读取属性**

获取到的均为属性的**字符串**

```html
<html>
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
	<select name="hobby" id="hobby" disabled>
		<option value="1">Basketball</option>
		<option value="2">Tennis</option>
		<option value="3">Football</option>
	</select>
<script type="text/javascript">
	var selectNode = document.getElementById("hobby");
	var isSelectDisabled = selectNode.getAttribute("disabled");	//String类型, "true"
	// alert(typeof(isSelectDisabled) == "string");	//true
	var selectId = selectNode.getAttribute("id");	//String类型，"hobby"
	// alert(typeof(selectId) == "string");	//true
	alert("Make a breakpoint here to see the liNodes value");
</script>
</body>
</html>
```

**写入属性**

可增加新的属性或改写已有属性

```html
<html>
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
	<select name="hobby" id="hobby">
		<option value="1">Basketball</option>
		<option value="2">Tennis</option>
		<option value="3">Football</option>
	</select>
<script type="text/javascript">
	var optionNodes = document.querySelectorAll("#hobby option");
	/* 修改已有属性 */
	optionNodes[0].setAttribute("value", "Basketball");
	optionNodes[1].setAttribute("value", "Tennis");
	optionNodes[2].setAttribute("value", "Football");
	/* 增加新的属性 */
	optionNodes[0].setAttribute("class", "Basketball");
	optionNodes[1].setAttribute("class", "Tennis");
	optionNodes[2].setAttribute("class", "Football");
</script>
</body>
</html>
```

**特点**

- X 仅可获取字符串（使用时需转换）
- √ 通用性强

### dataset 来存储数据

自定义属性，其为 `HTMLElement` 上的属性也是 `data-*` 的属性集。主要用于在元素上保存数据。获取的均为**属性字符串**。数据通常使用 AJAX 获取并存储在节点之上。

```html
<html>
<head>
	<meta charset="utf-8">
	<title></title>
</head>
<body>
	<!-- data-userid 中的属性建议都用小写，因为即使你写data-userId，获取到得dataset中得属性还是userid -->
	<!-- 你用dataset.userId是无法获取到值的，只能用dataset.userid才能获取到 -->
	<div id='user' data-userid='1234' data-username='xxx' data-email='111@qq.com'></div>
<script type="text/javascript">
	var divNode = document.getElementById("user");
	var userId = divNode.dataset.userid;	//1234
	var username = divNode.dataset.username;	//xxx
	var email = divNode.dataset.email;	//111@qq.com
	alert("Make a breakpoint here to see the value");
</script>
</body>
</html>
```

NOTE：`dataset` 在低版本 IE 不可使用，但可通过 `getAttribute` 与 `setAttribute` 来做兼容。