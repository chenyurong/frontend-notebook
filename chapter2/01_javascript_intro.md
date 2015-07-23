<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [JavaScript 介绍](#javascript-%E4%BB%8B%E7%BB%8D)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## JavaScript 介绍

前端开发三要素，`HTML`（描述网页内容），`CSS`（描述样式），`JavaScript`（控制网页行为）。JavaScript 为解释型编程语言，运行环境也很广泛。

![](../img/J/javascript-history.png)

![](../img/J/javascript-env.png)

**JavaScript**的引入方法如下：

```javascript
<!DOCTYPE html>
<html>
<head>
  <title></title>
</head>
<body>

  <!-- 以上代码忽略 -->

  <!-- 需将 javascript 代码放置在 body 标签的最末端 -->
  <!-- 外联文件 -->
  <script src="/javascripts/application.js" type="text/javascript" charset="utf-8" async defer></script>
  <!-- 内嵌代码 -->
  <script>
    console.log('>>> Hello, world!');
  </script>
</body>
</html>
```