<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [页面优化](#%E9%A1%B5%E9%9D%A2%E4%BC%98%E5%8C%96)
  - [页面优化的好处](#%E9%A1%B5%E9%9D%A2%E4%BC%98%E5%8C%96%E7%9A%84%E5%A5%BD%E5%A4%84)
  - [如何优化](#%E5%A6%82%E4%BD%95%E4%BC%98%E5%8C%96)
    - [减少HTTP请求](#%E5%87%8F%E5%B0%91http%E8%AF%B7%E6%B1%82)
    - [减少文件大小](#%E5%87%8F%E5%B0%91%E6%96%87%E4%BB%B6%E5%A4%A7%E5%B0%8F)
    - [页面性能](#%E9%A1%B5%E9%9D%A2%E6%80%A7%E8%83%BD)
    - [可读性，可维护性](#%E5%8F%AF%E8%AF%BB%E6%80%A7%EF%BC%8C%E5%8F%AF%E7%BB%B4%E6%8A%A4%E6%80%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 页面优化

### 页面优化的好处

- 提升网页响应速度
- 对搜索引擎、屏幕阅读器友好
- 提高可读性，可维护性

### 如何优化

- 减少HTTP请求
- 减少文件大小
- 提升页面性能
- 提高代码可读性和可维护性

#### 减少HTTP请求

- 图片合并

	- 把可以合并为一张图片的图片合并

- CSS文件合并
	- 多个CSS文件合并为一个
	- 如果页面样式少，可以把少量CSS样式内联
	- 避免使用import的方式引入css文件（@import "base.css"）
	
NOTE：因为每个import都会产生一个请求，而且请求是同步的。

#### 减少文件大小

- 选择合并的图片格式（PNG/JPG/）
- 压缩图片（可以用ImageOptim/ImageAlpha/JPEGmini等软件）
- CSS值缩写（如：margin: 5px 10px;）
- 省略值为0的单位（如：marin: 0px 10px -> margin:0 10px）
- 颜色值最短表示（red & rgb(255,255,0) & rgba(0,0,0,0.5) & #ccc）
- CSS选择器合并（将同样功能的样式合并）
- 将CSS文件中得空格压缩（可以用YUI Compressor/cssmin等）

NOTE：可以进行值缩写的还有margin/padding/border/border-radius/font/background

#### 页面性能

- 加载顺序
	- 把`<link rel="" href="">`放在<head>元素中
	- JS脚本建议放在<body>元素底部
- 减少标签数量
- 选择器长度（以最短能够选择到元素为标准）
- 减少耗性能属性的使用（如:expression()、filter()、border-radius、box-shadow、gradients）
- 给图片设置宽高，并且不要对图片进行缩放
- 所有表现用切换CSS Class实现
 
NOTE：选择器过长会影响CSS对于元素的查找

#### 可读性，可维护性

- 规范
制定编写开发规范
- 语义化
使用语义化的标签书写代码
- 尽量避免Hack
- 模块化
- 注释