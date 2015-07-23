<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [文档树](#%E6%96%87%E6%A1%A3%E6%A0%91)
- [My header](#my-header)
    - [文档节点（DOM Note）](#%E6%96%87%E6%A1%A3%E8%8A%82%E7%82%B9%EF%BC%88dom-note%EF%BC%89)
      - [文档节点类型](#%E6%96%87%E6%A1%A3%E8%8A%82%E7%82%B9%E7%B1%BB%E5%9E%8B)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 文档树

Document Object Model (DOM) ，即文档**对象**模型，其用对象的方式表示对应的文档结构及内容。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>My title</title>
  </head>
  <body>
    <a href="">My Link</a>
    <h1>My header</h1>
  </body>
</html>
```

**DOM 树的核心内容**

- DOM Core  DOM核心结构，API的定义
- DOM HTML  定义HTML如何转换成对象
- DOM Style  定义如何把样式转换成对象
- DOM Event  事件模型

![](../img/D/dom-tree.gif)

通过使用 DOM 提供的 API (Application Program Interface) 可以动态的修改节点（node），也就是对 DOM 树的直接操作。浏览器中通过使用 JavaScript 来实现对于 DOM 树的改动。

### 文档节点（DOM Note）

#### 文档节点类型

**常用节点类型**

- ELEMENT_NODE 元素节点

可使用 `document.createElement('elementName');`创建

- TEXT_NODE 元素节点

可使用 `document.createTextNode('Text Value');` 创建

```html
var bodyNode = document.getElementsByTagName("body")[0]; //Get the <body> node
var pNode = document.createElement("p");	//create a new <p> node
var txtNode = document.createTextNode("Here is the text content"); //create a new text node
divNode.appendChild(txtNode);
bodyNode.appendChild(divNode);
//可以通过element.nodeType获取一个节点的节点类型
//alert(bodyNode.nodeType); //1 	Element
//alert(pNode.nodeType);	//1		Text
//alert(txtNode.nodeType); //3	Text
```

**不常用节点类型**

- COMMENT_NODE
- DOCUMENT_TYPE_NODE

**不同节点对应的NodeType类型**

|节点编号|节点名称|
|---|--|
|1|Element|
|2|Attribute|
|3|Text|
|4|CDATA Section|
|5|Entity Reference|
|6|Entity|
|7|Processing Instrucion|
|8|Comment|
|9|Document|
|10|Document Type|
|11|Document Fragment|
|12|Notation|

NOTE：要清楚`节点`和`元素`的区别。我们平常说的`元素`其实指的是节点中的`元素节点`。所以说`节点`不仅包含`元素节点`，还包括`文本节点`、`实体节点`等。
