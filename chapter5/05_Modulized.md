<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [技术选型 - 模块化](#%E6%8A%80%E6%9C%AF%E9%80%89%E5%9E%8B---%E6%A8%A1%E5%9D%97%E5%8C%96)
  - [语言的模块支持](#%E8%AF%AD%E8%A8%80%E7%9A%84%E6%A8%A1%E5%9D%97%E6%94%AF%E6%8C%81)
  - [模块](#%E6%A8%A1%E5%9D%97)
    - [反模式](#%E5%8F%8D%E6%A8%A1%E5%BC%8F)
    - [字面量的模式（对象写法）](#%E5%AD%97%E9%9D%A2%E9%87%8F%E7%9A%84%E6%A8%A1%E5%BC%8F%EF%BC%88%E5%AF%B9%E8%B1%A1%E5%86%99%E6%B3%95%EF%BC%89)
    - [IIFE（Immediately-invoked Function Expression）](#iife%EF%BC%88immediately-invoked-function-expression%EF%BC%89)
    - [命名空间](#%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4)
  - [模块系统](#%E6%A8%A1%E5%9D%97%E7%B3%BB%E7%BB%9F)
    - [CommonJS/Module规范](#commonjsmodule%E8%A7%84%E8%8C%83)
    - [AMD模块化标准](#amd%E6%A8%A1%E5%9D%97%E5%8C%96%E6%A0%87%E5%87%86)
    - [ES6/Module规范](#es6module%E8%A7%84%E8%8C%83)
    - [SystemJS/Module Demo](#systemjsmodule-demo)
    - [对比](#%E5%AF%B9%E6%AF%94)
    - [参考资料](#%E5%8F%82%E8%80%83%E8%B5%84%E6%96%99)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 技术选型 - 模块化

### 语言的模块支持

这里的模块组织指的是Javascript的模块组织

```java
java:import
C#:using
css:@import
javascript:None!
```

其他语言如java，C#，CSS等都由其模块支持，但是javascript却没有

### 模块

**模块的职责**

1. 封装实现
2. 暴露接口
3. 声明依赖 

从上面模块的职责中可以看出，衡量一种模式好坏的标准就是看它**是否很好地实现了封装、是否清晰地暴露出接口、是否声明了依赖**。

#### 反模式

即没有应用任何模块系统

```javascript
//math.js
function add(a, b){
	return a + b;
}
function sub(a, b){
	return a - b;
}
```

```javascript
//caculator.js
var action = "add";
function compute(a, b){
	switch(action){
		case "add": return add(a, b);
		case "sub": return add(a, b);
	}
}
```

上面的math.js和caculator.js存下以下的不足：   

math.js -> 封装性差，没有进行访问控制；接口暴露不明显；   
caculator.js -> 没有依赖声明；使用了全局状态（action）

#### 字面量的模式（对象写法）

```javascript
//math.js
var math = {
	add: function add(a, b){
		return a + b;
	},
	sub: function sub(a, b){
		return a - b;
	}
}
```

```javascript
//caculator.js
var caculator = {
	action: "add",
	compute: function compute(a, b){
		switch(action){
			case "add": return math.add(a, b);
			case "sub": return math.sub(a, b);
		}
	}
}
```
math.js -> 封装性差，没有进行访问控制；接口暴露明显，接口结构性好   
caculator.js -> 没有依赖声明

#### IIFE（Immediately-invoked Function Expression）

自执行函数表达式

```javascript
///caculator-1.js
var caculator = (function(){
	var action = "add"
	return {
		compute: function(a, b){
			switch(action){
				case "add":
				  return math.add(a, b)
				case "sub":
				  return math.sub(a, b)
			}
		}
	}
})();
```

caculator-1.js -> 接口暴露明显，接口结构性好；有访问控制；但还是没有依赖声明

```javascript
//caculator-2.js
var caculator = (function(m){
	var action = "add";
	function compute(a, b){
		switch(action){
			case "add":
			  return m.add(a, b)
			case "sub":
			  return m.sub(a, b)
		}
	}
	return{
		compute: compute;
	}
})(math);
```

caculator-2.js -> 接口暴露明显，接口结构性好；有访问控制；显式依赖声明；   

存在不足：仍然污染了全局变量；必须手动进行依赖管理

#### 命名空间

```javascript
//math.js
//namespace(name, dependencyModule, code)
namespace("math", [], function(){
	function add(a, b){return a + b;}
	function sub(a, b){return a - b;}
	return{
		add: add,
		sub: sub
	}
})
```

```javascript
//caculator.js
namespace("caculator", ["math"], function(m){
	var action = "add";
	function compute(a, b){
		return m[action](a, b);
	}
	return{
		compute: compute
	}
})
```

但是命名空间还是没有解决模块管理的问题

### 模块系统

**模块系统的职责**

1. 进行依赖管理（加载/分析/注入/初始化）
2. 决定模块写法

#### CommonJS/Module规范

```javascript
//math.js
function add(a, b){
	return a + b;
}
function sub(a, b){
	return a - b;
}
exports.add = add;
exports.sub = sub;
```

```javascript
//caculator.js
var math = require("./math"); //依赖声明
function Caculator(container){
	this.left = container.querySelector(".j-left");
	this.right = container.querySelector(".j-right");
	this.add = container.querySeletor(".j-add");
	this.result = container.querySelector(".j-result");
	this.add.addEventListener("click", this.compute.bind(this));
}
Caculator.prototype.compute = function(){
	this.result.textContent = math.add(this.left.value, this.right.value)
}
exports.Caculator = Caculator; //接口暴露
```

优点：

1. 依赖管理成熟可靠
2. 社区活跃
3. 运行时支持，模块定义非常简单
4. 文件级的模块作用域隔离
5. 可以处理循环依赖

缺点：

1. 不是标准组织的规范
2. 同步的require，没有考虑浏览器环境

用browserify可以帮助我们把多个JS文件打包成一个JS文件

#### AMD模块化标准

天然地作用于异步通信

```javascript
//math.js
define([], function(){
	function add(a, b){
		return a + b;
	}
	function sub(a, b){
		return a - b;
	}
	return{		//暴露接口
		add: add,
		sub: sub
	}
})
```

```javascript
//caculator.js
define(["./math"], function(math){
	function Caculator(container){
	this.left = container.querySelector(".j-left");
	this.right = container.querySelector(".j-right");
	this.add = container.querySeletor(".j-add");
	this.result = container.querySelector(".j-result");
	this.add.addEventListener("click", this.compute.bind(this));
	//....略
}
Caculator.prototype.compute = function(){}
return{
	Caculator: Caculator
}
})
```

AMD有一个完整组件，即结构+逻辑+样式的组件。它可以加载html、css资源等，叫Loader Plugins。

优点：   
1. 依赖管理成熟可靠   
2. 社区活跃，规范接受度高   
3. 专为异步IO环境打造，适合浏览器环境   
4. 支持类似CommonJS的书写方式   
5. 通过插件API可支持加载非JS资源   
6. 成熟的打包构建工具，并可结合插件   

缺点：   
1. 模块定义繁琐，需要额外嵌套  
2. 只是库级别支持，需要引入额外库   
3. 无法处理循环依赖   
4. 无法实现条件加载   

#### ES6/Module规范

```javascript
//math.js
function add(a, b){
	return a + b;
}
function sub(a, b){
	return a - b;
}
export{add, sub}  //export关键字接口暴露
```

```javascript
//caculator.js
import{add} from "./math"; //引入依赖
class Caculator{
	constructor(container){
		this.left = container.querySelector(".j-left");
		this.right = container.querySelector(".j-right");
		this.add = container.querySeletor(".j-add");
		this.result = container.querySelector(".j-result");
		this.add.addEventListener("click", this.compute.bind(this));
	}
	compute(){
		this.result.tetContent
		  = add{this.left.value, this.right.value}
	}
}
export{Caculator}
```

优点：

1. 真正的规范，未来的模块标准
2. 语言级别的关键字支持
3. 适应所有javascript运行时，包括浏览器
4. 同样可以处理循环依赖

缺点：

1. 规范并未达到未定级别
2. 基本还没有浏览器支持
3. 鲜有项目支持

#### SystemJS/Module Demo

是一个统一的动态Loader。它支持AMD，支持加载CommonJs，支持加载ES6，支持Transpiler，可支持任意资源。

```javascript
System.paths = {
    "app/*" : "../commonjs/*.js"
    "app/*" : "../amd/*.js"
	"app/*" : "../es6/*.js"
}
System.import("app/caculator").then(function(c){
	new c.Caculator(document.getElementById(("caculator")))
});
```

```javascript
//caculator.js
import{add} from "./math"; //引入依赖
class Caculator{
	constructor(container){
		this.left = container.querySelector(".j-left");
		this.right = container.querySelector(".j-right");
		this.add = container.querySeletor(".j-add");
		this.result = container.querySelector(".j-result");
		this.add.addEventListener("click", this.compute.bind(this));
	}
	compute(){
		this.result.tetContent
		  = add{this.left.value, this.right.value}
	}
}
export{Caculator}
```

#### 对比

IIFE / AMD / Commonjs / ES6

#### 参考资料

1. [Javascript模块化编程（一）：模块的写法](http://www.ruanyifeng.com/blog/2012/10/javascript_module.html)
2. [Javascript模块化编程（二）：AMD规范](http://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html)
3. [Javascript模块化编程（三）：require.js的用法](http://www.ruanyifeng.com/blog/2012/11/require_js.html)
4. [前端模块化开发的价值](https://github.com/seajs/seajs/issues/547)
5. [Why SeaJS - 万神劫 - Chaos的Blog](http://chaoskeh.com/blog/why-seajs.html) 





 











