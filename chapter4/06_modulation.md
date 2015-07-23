<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [模块化](#%E6%A8%A1%E5%9D%97%E5%8C%96)
  - [什么是模块化](#%E4%BB%80%E4%B9%88%E6%98%AF%E6%A8%A1%E5%9D%97%E5%8C%96)
  - [为什么要模块化](#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E6%A8%A1%E5%9D%97%E5%8C%96)
  - [如何实现模块化](#%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E6%A8%A1%E5%9D%97%E5%8C%96)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 模块化

### 什么是模块化

- 一系列相关联的结构组成的整体
- 带有一定语义，而非表现

如下面的翻页器和图片轮播模块：

![](../img/M/modulized-example.png)

### 为什么要模块化

- 模块化后代码可读性高、可维护性好
- 模块化利于多人协同开发
- 便于扩展和重用
- 可以避免样式污染的问题

### 如何实现模块化

1. 以模块分类命名（如：m-, md-）
2. 以一个主选择器开头（模块根节点）
3. 使用以主选择器开头的后代选择器（模块子节点）

```
<!-- 模块1 -->
<模块1>
	<子元素1></子元素1>
	<子元素2></子元素2>
</模块1>
<!-- 模块2 -->
<模块2>
	<子元素1></子元素1>
	<子元素2></子元素2>
</模块2>
<style>
	/* 模块1 */
	模块1{}
	模块1 子元素1{}
	模块1 子元素2{}
	/* 模块2 */
	模块2{}
	模块2 子元素1{}
	模块2 子元素2{}
</style>
```

**模块例子**
```
<!-- NAV MODULE -->
<div class="m-nav">
	<ul>
		<li class="z-crt"><a href=""></a></li>
		<li><a href=""></a></li>
	</ul>
</div>
<!-- /NAV MODULE -->
<style type="text/css">
	/* 导航模块 */
	.m-nav{}  /* 模块容器 */
	.m-nav li, .m-nav a{}
	.m-nav li{}
	.m-nav a{}
	.m-nav .z-crt a{} /* 交互状态变化 */
</style>
```

**模块扩展的例子**

只需在原来的基础上加上新的class样式进行拓展即可。

```
<!-- NAV-1 MODULE -->
<div class="m-nav m-nav-1">
	<ul>
		<li class="z-crt"><a href=""></a></li>
		<li><a href=""></a></li>
	</ul>
</div>
<!-- /NAV-1 MODULE -->
<style type="text/css">
	/* 导航模块扩展 */
	.m-nav-1{}
	.m-nav-1 a{border-radius: 5px;}
	.m-nav-1 .btn{}
</style>
```