<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [基本语法](#%E5%9F%BA%E6%9C%AC%E8%AF%AD%E6%B3%95)
  - [变量标示符](#%E5%8F%98%E9%87%8F%E6%A0%87%E7%A4%BA%E7%AC%A6)
  - [关键字与保留字](#%E5%85%B3%E9%94%AE%E5%AD%97%E4%B8%8E%E4%BF%9D%E7%95%99%E5%AD%97)
  - [字符敏感](#%E5%AD%97%E7%AC%A6%E6%95%8F%E6%84%9F)
  - [严格模式](#%E4%B8%A5%E6%A0%BC%E6%A8%A1%E5%BC%8F)
  - [注释](#%E6%B3%A8%E9%87%8A)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 基本语法

### 变量标识符

- 第一个字符必须是一个字母、下划线（_）或一个美元符号（$）
- 其他字符可以是字母、下划线、美元符号或数字

```javascript
var _name = null;
var $name = null;
var name0 = null;
```

### 关键字与保留字

JavaScript 在语言定义中保留的字段，这些字段在语言使用中存在特殊意义或功能，在程序编写的过程中不可以当做变量或函数名称使用。无需记忆，报错修改即可。

```
//ECMAScript的全部关键字
break	else	new		var
case	finally	return	void
catch 	for		switch	while
continue	function	this	with
default		if			throw	
delete		in			try
do			instanceof	typeof
//ECMA-262第3版定义的所有保留字
abstract	enum	int		short
boolean 	export	interface	static
byte		extends	long		super
char		final	native		synchronized
class		float	package		throws
const		goto	private		transient
debugger	implements	protected	volatile
double 		import	public
```

### 字符敏感

字符串的大小写是有所区分的，不同字符指代不同的变量。

### 严格模式

**增益**

- 消除语法中不合理与不安全的问题，保证代码正常运行
- 提高编译效率，增加运行速度

**使用方法**

```javascript
<!-- 全局使用 严格 模式 -->
"use strict";
(function(){
  console.log('>>> Hello, world!');
})()

<!-- 或者在函数内部声明使用 严格 模式 -->
(function(){
  "use strict";
  console.log('>>> Hello, world!');
})()
```

严格模式与标准模式的区别：

- 严格模式下隐式声明或定义变量被静止
- 严格模式下对象重名的属性在严格模式下被静止
- 严格模式下 `arguments.callee()` 被禁用
- 严格模式下 `with()` 语句
- 更多限制

### 注释

```javascript
/*
  多行注释，不可嵌套
 */

// 单行注释
```

### JavaScript中的参数

ECMAScript函数的参数与大多数其他语言中的函数参数有所不同，ECMAScript函数不介意床底多少个参数，也不在乎传进来的参数是什么数据类型。

```
//普通函数
function sayHi(name, message){
	alert("Hello " + name + message);
}
//用arguments获取参数
function sayHi(){
	alert("Hello " + arguments[0] + arguments[1]);
}
```

上面两个函数都是合法并且功能相同的。这个事实说明了ECMAScript函数的一个重要特点：命名的参数只是提供便利，但不是必须的。

NOTE：ECMAScript中的所有参数传递都是值，不可能通过引用传递参数。




