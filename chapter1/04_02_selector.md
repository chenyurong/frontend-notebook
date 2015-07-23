<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [选择器](#%E9%80%89%E6%8B%A9%E5%99%A8)
  - [简单选择器](#%E7%AE%80%E5%8D%95%E9%80%89%E6%8B%A9%E5%99%A8)
    - [标签选择器](#%E6%A0%87%E7%AD%BE%E9%80%89%E6%8B%A9%E5%99%A8)
    - [类选择器](#%E7%B1%BB%E9%80%89%E6%8B%A9%E5%99%A8)
    - [id 选择器](#id-%E9%80%89%E6%8B%A9%E5%99%A8)
    - [通配符选择器](#%E9%80%9A%E9%85%8D%E7%AC%A6%E9%80%89%E6%8B%A9%E5%99%A8)
    - [属性选择器](#%E5%B1%9E%E6%80%A7%E9%80%89%E6%8B%A9%E5%99%A8)
    - [伪类选择器](#%E4%BC%AA%E7%B1%BB%E9%80%89%E6%8B%A9%E5%99%A8)
  - [伪元素选择器](#%E4%BC%AA%E5%85%83%E7%B4%A0%E9%80%89%E6%8B%A9%E5%99%A8)
    - [first-letter](#first-letter)
    - [first-line](#first-line)
    - [before](#before)
    - [after](#after)
    - [selection](#selection)
  - [组合选择器](#%E7%BB%84%E5%90%88%E9%80%89%E6%8B%A9%E5%99%A8)
    - [后代选择器](#%E5%90%8E%E4%BB%A3%E9%80%89%E6%8B%A9%E5%99%A8)
    - [子选择器](#%E5%AD%90%E9%80%89%E6%8B%A9%E5%99%A8)
    - [兄弟选择器](#%E5%85%84%E5%BC%9F%E9%80%89%E6%8B%A9%E5%99%A8)
  - [选择器分组](#%E9%80%89%E6%8B%A9%E5%99%A8%E5%88%86%E7%BB%84)
  - [继承、优先、层级](#%E7%BB%A7%E6%89%BF%E3%80%81%E4%BC%98%E5%85%88%E3%80%81%E5%B1%82%E7%BA%A7)
    - [继承](#%E7%BB%A7%E6%89%BF)
    - [优先](#%E4%BC%98%E5%85%88)
    - [层叠](#%E5%B1%82%E5%8F%A0)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 选择器

选择器可被看做表达式，通过它可以选择相应的元素并应用不同的样式。

- 简单选择器
- 元素选择器
- 组合选择器

#### 简单选择器

##### 标签选择器

直接以html中标签名作为选择器名的都叫标签选择器。

```html
<div>
  <p>Sample Paragraph</p>
  <p>Sample Paragraph</p>
  <p>Sample Paragraph</p>
</div>

<style type="text/css">
  p {
    color: blue;
  }
</style>
```

##### 类选择器

`.className` 以 `.` 开头，名称可包含字母、数字、`-`、`_`，但必须以字母开头。它区分大小写并可出现多次。

```html
<div>
  <p>Sample Paragraph</p>
  <p class="special bold">Sample Paragraph</p>
  <p>Sample Paragraph</p>
</div>

<style type="text/css">
  .special {
    color: orange;
  }
  .bold {
    font-weight: bold;
  }
</style>
```

##### id 选择器

`#idName` 以 `#` 开头且只可出现**一次**，其命名要求与 `.className` 相同。

```html
<div>
  <p id="special">Sample Paragraph</p>
</div>

<style type="text/css">
  #special {
    color: red;
  }
</style>
```

##### 通配符选择器

用于选中所有`标签选择器`

```html
<div>
  <!-- <p>和<span>标签中的字体都将是蓝色的 -->
  <p>Sample Paragraph</p>
  <span>Sample Paragraph</span>
</div>

<style type="text/css">
  * {
    color: blue;
  }
</style>
```

##### 属性选择器

###### attr或attr=val

选中拥有attr属性或attr属性的值为val的元素。

```html
<html>
<head>
	<title>Test</title>
</head>
<body>
<div>
  <form action="">
    <input type="text" value="ShuYi" disabled><br>
    <input type="password" placeholder="password"><br>
    <input type="button" value="button">
  </form>
</div>
<style type="text/css">
  /* 选中第一个<input>标签 */
  [disabled] {
    background-color: orange;
  }
  /* 选中第二个<input>标签 */
  [type=password] {
    background-color: pink;
  }
</style>
</body>
</html>
```
###### attr~=val

选中attr属性中包含 `val` 属性值的元素。  

`[class~=sports]` 选中class属性包含sports的元素

```html
<html>
<head>
	<title>Test</title>
</head>
<body>
<div>
  <form action="">
    <input type="text" class="a b d" value="ShuYi"><br> <!-- 黑底白字 -->
    <input type="password" class="c" value="password"><br> <!-- 橙底白字 -->
    <input type="button" value="button">
  </form>
</div>
<style type="text/css">
  	/* 选中第一个<input>标签 */
	[class~=a]{
		background-color: black;
		color: white;
	}
	/* 选中第二个<input>标签 */
	[class~=c]{
		background-color: orange;
		color: white;
	}
</style>
</body>
</html>
```

###### attr*=val

选中attr属性值中包含`val`的元素，如果值中又符号或空格则需要使用引号 `""`。

```html
<html>
<head>
	<title>Test</title>
</head>
<body>
<div>
  <form action="">
    <a href="http://lady.163.com">Lady</a><br> <!-- 蓝色 --> 
    <a href="http://lady.163.com/chapter1">Lady/chapter1</a><br> <!-- 蓝色 -->
    <a href="http://tech.163.com">tech</a><br> <!-- 红色 -->
    <a href="">default color link</a> <!-- 黑色 -->
  </form>
</div>
<style type="text/css">
  /* attr*=val  选中attr属性中包含 val 属性值的元素 */
	[href*="lady.163.com"]{
		color: blue;
	}
	[href*="tech.163.com"]{
		color: red;
	}
	/* 默认是黑色 */
	a{
		color: black;
	}
</style>
</body>
</html>
```
###### attr~=val 对比 attr*=val

两者虽然都会判断attr属性中是否包含val值，但是他们的侧重点（判断方式）是不同的。

- attr~=val 判断时会将attr的属性值用<kbd>空格</kbd>分成若干个值，之后判断这些值是否等于val。
- attr*=val 判断时直接将attr的值作为一个字符串，判断这个字符串是否包含val子串。

```html
<html>
<head>
	<title>Test</title>
</head>
<body>
<div>
  <form action="">
    <a href="http://lady.163.com">Lady</a><br>
    <a href="http://lady.163.com/chapter1">Lady/chapter1</a><br>
    <a href="http://tech.163.comd sdfd">tech</a><br>
    <a href="">default color link</a>
  </form>
</div>
<style type="text/css">
	[href~="lady.163.com"]{
		color: blue;
	}
	[href~="tech.163.com"]{
		color: red;
	}
	/* 默认是黑色 */
	a{
		color: black;
	}
</style>
</body>
</html>
```

上面例子的属性选择器没有选择到对应的元素，因此运行结果4个链接的文字颜色都是黑色的。而我们将href的属性值修改一下，改成下面这样：

```html
<html>
<head>
	<title>Test</title>
</head>
<body>
<div>
  <form action="">
  	<!-- 蓝色 -->
    <a href="http://lady.163.com lady.163.com">Lady</a><br>
    <!-- 蓝色 -->
    <a href="http://lady.163.com/chapter1 lady.163.com">Lady/chapter1</a><br>
    <!-- 红色 -->
    <a href="http://tech.163.comd tech.163.com">tech</a><br>
    <!-- 黑色 -->
    <a href="">default color link</a>
  </form>
</div>
<style type="text/css">
	[href~="lady.163.com"]{
		color: blue;
	}
	[href~="tech.163.com"]{
		color: red;
	}
	/* 默认是黑色 */
	a{
		color: black;
	}
</style>
</body>
</html>
```

运行代码会发现前两个链接是蓝色的，第三个链接是红色的，第四个链接是默认的黑色。这正好验证了上面的结论。即：attr~=val 判断时会将attr的属性值用<kbd>空格</kbd>分成若干个值，之后判断这些值是否等于val。有时间的同学可以自行再验证一下`attr*=val`。

###### attr|=val

选中attr属性值中以`val-`开头的元素。

```html
<html>
<head>
	<title>Test</title>
</head>
<body>
<div>
  <form action="">
    <a href="##chapter1">Lady</a><br> <!-- 黑色 -->
    <a href="#-chapter2">Lady/chapter1</a><br> <!-- 蓝色 -->
    <a href="">default color link</a> <!-- 黑色 -->
  </form>
</div>
<style type="text/css">
	[href|="#"]{
		color: blue;
	}
	/* 默认是黑色 */
	a{
		color: black;
	}
</style>
</body>
</html>
```

###### attr^=val

选中attr属性值中以`val`开头的元素，如果值为符号或空格则需要使用引号 `""`。

`[href^="#"]` 选中href属性值以`#`开头的元素

###### attr$=val

选中attr属性值中以`val`结尾的元素，如果值为符号或空格则需要使用引号 `""`。

`[href$=pdf]` 选中ref属性值以`pdf`结尾的元素

```html
<html>
<head>
	<title>Test</title>
</head>
<body>
<div>
  <form action="">
    <a href="##chapter1">Lady</a><br> <!-- 蓝色 -->
    <a href="JavaScriptDesign.pdf">Lady/chapter1</a><br> <!-- 红色 -->
    <a href="">default color link</a> <!-- 黑色 -->
  </form>
</div>
<style type="text/css">
	[href^="##"]{
		color: blue;
	}
	[href$=".pdf"]{
		color: red;
	}
	/* 默认是黑色 */
	a{
		color: black;
	}
</style>
</body>
</html>
```

##### 伪类选择器

###### 常用伪类选择器

- `:link` 选中所有href属性值不为空的<a>标签，只适用于`<a>`标签，IE6+
- `:visited` 选中所有已被访问过的<a>标签，只适用于`<a>`标签，IE7+
- `:hover` 悬停在元素上时，IE6
- `:active` 点击时，IE9+
- `:enabled` 可用时，IE9+
- `:disabled` 不可用时，IE9+
- `:checked` 被选中时，IE9+
- `:first-child` 第一个子元素，IE8+
- `:last-child` ，IE9+
- `:nth-child(even)` 可为 `odd` `even` 或数字，IE9+
- `:nth-last-child(n)` `n`从 0 开始计算，IE9+
- `:only-child` 仅选择唯一的元素，IE9+
- `:only-of-type`，IE9+
- `:first-of-type`，IE9+
- `:last-of-type`，IE9+
- `:nth-of-type(even)`，IE9+
- `:nth-last-of-type(2n)`，IE9+

###### 不常用伪类选择器

- `:empty` 选中页面中无子元素的标签，IE9+
- `:root` 选择 HTML 根标签，IE9+
- `:not()` 参数为一般选择器，IE9+
- `:target` 被锚点选中的目标元素，IE9+
- `:lang()` 选中语言值为某类特殊值的元素，IE7+

NOTE：`element:nth-of-type(n)` 指父元素下第 n 个 `element` 元素，`element:nth-child(n)` 指父元素下第 n 个元素且元素为 `element`，若不是，选择失败。具体细节请在使用时查找文档。

【MARK1 整理一片关于伪类选择器使用的文章】

```html
<div>
  <a href="http://sample-site.com" title="Sample Site">Sample Site</a>
</div>
<style type="text/css">
  /* 伪类属性定义有顺序要求！ */
  a:link {
    color: gray;
  }
  a:visited {
    color:red;
  }
  a:hover {
    color: green;
    /* 鼠标悬停 */
  }
  a:active {
    color: orange;
    /* 鼠标点击 */
  }
</style>
```

#### 伪元素选择器

注意与伪类选择器的区分。（伪类选择器只有一个`:`号，而伪元素选择器有两个）

NOTE：注意元素符号和伪元素选择器中间不能有空格，如：`p ::first-letter`是错误的，`p::first-letter`才是正确的。

##### first-letter

`::first-letter`，选中第一个字符

```html
<html>
<head>
	<meta charset="utf-8">
	<title>Test</title>
	<style type="text/css">
		p{
			font-size: 20px;
		}
		p::first-letter{
			font-size: 40px;
		}
	</style>
</head>
<body>
	<p>Hello World!</p>
</body>
</html>
```

##### first-line

`::first-line`，选中第一行

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>伪元素选择器——::first-line</title>
	<style type="text/css">
		.w300{width: 300px;}
		.w300 p{color: black;}
		.w300 p::first-line{font-weight: bold;}
	</style>
</head>
<body>
	<div class="w300">
		<p>Hello World.Hello World.Hello World.Hello World.Hello World.Hello World.</p>
	</div>
</body>
</html>
```

##### before

`::before{content: "before"}`，在元素前加上content值， 需与 `content` 一同使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>伪元素选择器——::before</title>
	<style type="text/css">
		p{width: 500px; border: 1px solid red; color: blue;}
		p::before{content: "Before the Main Content";} /* 将内容插到指定元素前 */
	</style>
</head>
<body>
	<p>Main Content</p>
</body>
</html>
```

##### after

`::after{content: "after"}`，在元素后加上content值，需与 `content` 一同使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>伪元素选择器——::before</title>
	<style type="text/css">
		p{width: 500px; border: 1px solid red; color: blue;}
		p::after{content: "***Extra Part***";} /* 将内容插到指定元素前 */
	</style>
</head>
<body>
	<p>Main Content</p>
</body>
</html>
```

##### selection

`::selection`，被用户选中的内容（鼠标选择高亮属性）

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>伪元素选择器——::selection</title>
	<style type="text/css">
		/* 选中文字为黑底白字 */
		p::selection{background-color: black; color: white;}
	</style>
</head>
<body>
	<p>Hello World.Hello World.Hello World.Hello World.Hello World.Hello World.</p>
</body>
</html>
```

#### 组合选择器

##### 后代选择器 

`.main span {...}` 使用` `（空格）表示

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>组合选择器-后代选择器</title>
	<style type="text/css">
		.main span{
			background-color: gray;
		}
	</style>
</head>
<body>
	<div class="main">
		<span>1.1</span>  <!-- 被选中-->
		<p>
			<span>2.1</span> <!-- 被选中 -->
		</p>
	</div>
</body>
</html>
```

##### 子选择器 

`.main>span {...}` 使用`>`表示

##### 兄弟选择器 

`h2+p {...}` 使用`+`表示（选中h2元素后紧邻的那个p元素）

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>组合选择器-后代选择器 A+B </title>
	<style type="text/css">
		span{display: block; line-height: 2;}
		span+p{color: red;}  
	</style>
</head>
<body>
	<div class="main">
		<span>0</span>
		<p>1</p>  <!-- 被选中 -->
		<p>2</p>
		<p>3</p>
		<p>4</p>
	</div>
</body>
</html>
```

`span~p {...}` 使用`~`表示（选中span元素后的p元素，无须紧邻）

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>组合选择器-后代选择器 A~B </title>
	<style type="text/css">
		span{display: block; line-height: 2;}
		span~p{color: red;}  
	</style>
</head>
<body>
	<div class="main">
		<span>0</span>
		<p>1</p>  	<!-- 被选中 -->
		<p>2</p>	<!-- 被选中 -->
		<p>3</p>	<!-- 被选中 -->
		<p>4</p>	<!-- 被选中 -->
	</div>
</body>
</html>
```

接下来看一个更加复杂的例子，这个例子可以让你深入理解兄弟选择器：

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>组合选择器-后代选择器 复杂的例子 </title>
	<style type="text/css">
		span{display: block; line-height: 2;}
		/* 弟p元素选中p元素后的的所有兄 */
		p~p{color: red;}  
		/*p+p{color: red;}*/
	</style>
</head>
<body>
	<div class="main">
		<p>0</p>	
		<p>1</p>  	<!-- 被选中 -->
		<p>2</p>	<!-- 被选中 -->
		<span>3</span>
		<p>4</p>	<!-- 被选中 -->
		<p>5</p>	<!-- 被选中 -->
	</div>
</body>
</html>
```

NOTE：第一个p元素因为其前面没有p元素，所以就没被选中。

#### 选择器分组

```html
<style type="text/css">
/* 下面两组样式声明效果一致 */
h1 {color: red;}
h2 {color: red;}
h3 {color: red;}

h1, h2, h3 {color: red;}
</style>
```

#### 继承、优先、层级

##### 继承

子元素继承父元素的样式，但并不是所有属性都是默认继承的。通过文档中的 `inherited: yes` 来判断属性是否可以自动继承。

![](../img/C/css-inherit-doc.png)

**自动继承属性**
- color
- font
- text-align
- list-style
- ...

**非继承属性**
- background
- border
- position
- ...

##### 优先

CSS Specificity Calculator 可以在[这里](http://specificity.keegan.st/)找到。更多关于 CSS 优先级别的信息可以在[这里](https://css-tricks.com/specifics-on-css-specificity/)找到（英文）。

计算方法：
- a = 行内样式
- b = id 选择器的数量
- c = 类、伪类的属性选择器的数量
- d = 标签选择器和伪元素选择器的数量

NOTE：从上到下优先级一次降低，且优先级高的样式会将优先级低的样式覆盖。大致公式（并不准确）如下。

```
value = a * 1000 + b * 100 + c * 10 + d
```

**改变优先级**

- 改变样式声明先后顺序
- 提升选择器优先级
- `!important`（慎用）

##### 层叠

层叠为相同属性根据优先级覆盖，如优先级相同则后面会覆盖前面的属性，而不同属性则会合并。
