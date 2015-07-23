<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [规范化](#%E8%A7%84%E8%8C%83%E5%8C%96)
- [](#)
- [
/* 值简写还是不简写 */
 or 
```

- 层级
	- 用缩进体现层级，提高可读性
	- 标签正确嵌套，但嵌套不宜太深

- 注释

团队内自己定义注释的方式，哪些地方需要注释，注释的开头和结尾格式，如：

```

](#-%E5%80%BC%E7%AE%80%E5%86%99%E8%BF%98%E6%98%AF%E4%B8%8D%E7%AE%80%E5%86%99-%0A-or-%0A%0A%0A--%E5%B1%82%E7%BA%A7%0A%09--%E7%94%A8%E7%BC%A9%E8%BF%9B%E4%BD%93%E7%8E%B0%E5%B1%82%E7%BA%A7%EF%BC%8C%E6%8F%90%E9%AB%98%E5%8F%AF%E8%AF%BB%E6%80%A7%0A%09--%E6%A0%87%E7%AD%BE%E6%AD%A3%E7%A1%AE%E5%B5%8C%E5%A5%97%EF%BC%8C%E4%BD%86%E5%B5%8C%E5%A5%97%E4%B8%8D%E5%AE%9C%E5%A4%AA%E6%B7%B1%0A%0A--%E6%B3%A8%E9%87%8A%0A%0A%E5%9B%A2%E9%98%9F%E5%86%85%E8%87%AA%E5%B7%B1%E5%AE%9A%E4%B9%89%E6%B3%A8%E9%87%8A%E7%9A%84%E6%96%B9%E5%BC%8F%EF%BC%8C%E5%93%AA%E4%BA%9B%E5%9C%B0%E6%96%B9%E9%9C%80%E8%A6%81%E6%B3%A8%E9%87%8A%EF%BC%8C%E6%B3%A8%E9%87%8A%E7%9A%84%E5%BC%80%E5%A4%B4%E5%92%8C%E7%BB%93%E5%B0%BE%E6%A0%BC%E5%BC%8F%EF%BC%8C%E5%A6%82%EF%BC%9A%0A%0A)
    - [文件规范](#%E6%96%87%E4%BB%B6%E8%A7%84%E8%8C%83)
      - [文件分类规范](#%E6%96%87%E4%BB%B6%E5%88%86%E7%B1%BB%E8%A7%84%E8%8C%83)
      - [文件引入规范](#%E6%96%87%E4%BB%B6%E5%BC%95%E5%85%A5%E8%A7%84%E8%8C%83)
      - [文件本身规范](#%E6%96%87%E4%BB%B6%E6%9C%AC%E8%BA%AB%E8%A7%84%E8%8C%83)
    - [注释规范](#%E6%B3%A8%E9%87%8A%E8%A7%84%E8%8C%83)
      - [块状注释](#%E5%9D%97%E7%8A%B6%E6%B3%A8%E9%87%8A)
      - [单行注释](#%E5%8D%95%E8%A1%8C%E6%B3%A8%E9%87%8A)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 规范化

用一个团队规范来约束团队成员编写的代码

- 文件规范
- 注释规范
- 命名规范
- 书写规范
- 其他规范（图片、html规范）

### 文件规范

- 文件分类
- 文件引入
- 文件本身

#### 文件分类规范

即文件的分类归档

- 通用类（包括自己写的样式、第三方库、自己写的UI控件）
- 业务类（音乐类产品可以分为专辑、歌手等不同分类）

#### 文件引入规范

- 行内样式（不推荐）
- 外联引入（`<link rel="stylesheet" href="css/style.css"/>`）
- 内敛引入（`<style>...</style>`）
- 避免在CSS中使用`@import`

#### 文件本身规范

- 文件名（如：由小写字母、数字、中划线组成）
- 编码（设置成UTF-8编码方式）

### 注释规范

- 块状注释
- 单行注释
- 行内注释

#### 块状注释

- 统一缩进
- 在被注释对象之上

```
/* 块状注释文字
 * 块状注释文字
 */
.mlist{
  width: 500px;
}
```

#### 单行注释

- 文字两端需空格
- 在被注释对象之上

```
/* 单行注释文字 */
.m-list li em { color: #666;}

#### 行内注释

- 文字两端需空格
- 在分号之后

```
.m-list li a{color:#333; /* 对color的行内注释 */}
```

### 命名规范

主要是CSS选择器的命名规范

- 分类命名
- 命名格式
- 语义化命名

#### 分类命名

```
<style type="text/css">
	/* 布局样式 用global的g开头 */
	.g-header{color: black;}
	/* 文章样式 */
	.m-article{color: blue;}
	.m-article .header{font-size: 12px;}
</style>
<!-- demo -->
...
	<div class="g-header">...</div>
	<div class="g-section">
		<div class="m-article">
			<div class="header">...</div>
		</div>
	</div>
	<div class="g-footer">...</div>
...
```

布局类的样式用g（global）开头，如：`.g-header` `.g-section` 等。   
模块内的样式用m（module）开头，如：`.m-article` 等

#### 命名格式

- 选择器名称以及选择器内容都小写

```
/* 大写选择器（不推荐） */
.LIST{FONT-SIZE: 12PX;}

/* 小写选择器 */
.list{ font-size: 12px; }
```

- 选择器长度

```
.subnavigator{font-size: 12px;}
/* 缩写名称（长度适中的缩写） */ 
.subnav{font-size: 12px;}
/* 再缩写 */
.sbnv{font-size: 12px;}
```

#### 语义化命名

- 以内容语义命名

```
/* 以结构命名（不推荐） */
.top{ font-size: 12px;}
.top .link{color: #333;}
/* 以内容语义命名（推荐） */
.nav{font-size: 12px;}
.nav .link{color: #333}
```

### 书写规范

即CSS的一些书写规范

- 单行与多行
- 空格与分号
- 属性顺序
- Hack方式
- 值格式

#### 单行与多行

```
/* 单行 */
.logo a{float:left; padding:0 10px;}
/* 多行 */
.logo a{
	float: left;
	padding: 0 10px;
}
```

#### 空格与分号

- 空格
	- 缩进（必须有缩进，2个或4个空格）
	- 规则内的空格（`.logo{width: 200px; height: 50px;）
- 分号
	- 保留最后一个属性值的分号

#### 属性顺序

一般是按属性的重要性按顺序书写，一般是先`显示属性`、后`自身属性`、最后`文本属性和其他修饰属性`。

|->|显示属性|自身属性|文本属性和其他修饰|   
||---|---|---|---|
||display|width|font|
||visibility|height|text-align|
||position|margin|text-decoration|
||float|padding|vertical-align|
||clear|border|white-space|
||list-style|overflow|color|
||top|min-width|background|

#### Hack方式

- 统一个浏览器的Hack方式   

|支持的浏览器|Hack方式|说明|
|---|---|---|
|IE6|_property:value|只对IE6有效|
|IE6/7|*property:value|只对IE6/7有效|

```
/* IE7显示#888，IE6显示#fff，其他浏览器显示#000 */
.m-list{color:#000; *color:#888; _color:#fff;}
```

- 不用滥用Hack   
Hack应该是最后的选择

#### 值格式

统一属性值的格式

- color
	- `white`
	- `#fff`（推荐）
	- `rgb(255,255,255)`
- url   
	- url地址要不要引号
	- 单引号还是双引号

### 其他规范

#### HTML 规范

- 文档声明

`<!DOCTYPE html>`  在文档首行顶格开始

- 闭合

闭合标签：`<div></div>`
自闭合标签：`<input>` or `<input/>` 二选一

- 属性

```
/* 单引号还是双引号 */
<h1 class="logo"></h1>  or <h1 class='logo'></h2>
/* 值简写还是不简写 */
<input readonly> or <input readonly="readonly">
```

- 层级
	- 用缩进体现层级，提高可读性
	- 标签正确嵌套，但嵌套不宜太深

- 注释

团队内自己定义注释的方式，哪些地方需要注释，注释的开头和结尾格式，如：

```
<!-- LOGO -->
<h1 class="logo"></h1>
<!-- /LOGO -->
```

- 大小写

一般标签、属性均小写

#### 图片规范

- 文件名称
	- 语义化
	- 长度适中
- 保留源文件
- 图片合并
	- 尽可能使用sprite技术
	- sprite图片可按模块、业务、页面来划分