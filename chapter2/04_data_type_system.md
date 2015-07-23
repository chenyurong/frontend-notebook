<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [类型系统](#%E7%B1%BB%E5%9E%8B%E7%B3%BB%E7%BB%9F)
  - [标准类型（6个）](#%E6%A0%87%E5%87%86%E7%B1%BB%E5%9E%8B%EF%BC%886%E4%B8%AA%EF%BC%89)
    - [Undefined](#undefined)
    - [Null](#null)
    - [String](#string)
    - [Number](#number)
    - [Boolean](#boolean)
    - [Object](#object)
    - [变量转换表](#%E5%8F%98%E9%87%8F%E8%BD%AC%E6%8D%A2%E8%A1%A8)
  - [对象类型](#%E5%AF%B9%E8%B1%A1%E7%B1%BB%E5%9E%8B)
    - [内置对象类型(9个)](#%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1%E7%B1%BB%E5%9E%8B9%E4%B8%AA)
      - [String](#string-1)
      - [Number](#number-1)
      - [Boolean](#boolean-1)
      - [Object](#object-1)
      - [Array](#array)
      - [Date](#date)
      - [Error](#error)
      - [Function](#function)
      - [RegExp](#regexp)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 类型系统

JS类型系统可以分为标准类型和对象类型，进一步标准类型又可以分为原始类型和引用类型，而对象类型又可以分为内置对象类型、普通对象类型、自定义对象类型。

![](../img/J/javascript-type-system.png)

<!-- ![](../img/J/javascript-variable-type.jpg) -->

### 标准类型（6个）

标准类型共包括了6个分别是：`undefined` `Null` `String` `Number`  `Boolean` `Object`。     
其中`undefined` `Null` `String` `Number`  `Boolean` 是原始类型，而`Object`是引用类型。其声明方式如下：

```javascript
var a;    //undefined
var b = document.getElementById("no_exist_element"); //null
var e = "str";     //String
var d = 1;    //Number
var c = true;    //Boolean
var f = {name : "Tom"};    //Object
```

**原始类型和引用类型的区别**

原始类型储存在栈（Stack）中储存变量的值，而引用类型在栈中保存的是所引用内容储存在堆（Heap）中的值。类似于指针的概念，引用类型并非储存变量真实数值而是地址，所以对已引用类型的复制其实只是复制了相同的地址而非实际的变量值。

#### Undefined 

值：undefined    

出现场景：

- 以声明为赋值的变量 `var obj;`
- 获取对象不存在的属性 `var obj = {x: 0}; obj.y;`
- 无返回值函数的执行结果 `function f(){}; var obj = f();`
- 函数参数没有传入 `function f(i){console.log(i)}; f();`
- `void(expression)`

#### Null

值：null    

出现场景：

- 获取不存在的对象 `document.getElementById('not-exist-element')`

#### String 

值：字符串 出现场景：

- `var str = 'Hello, world!';`

#### Number 

值：整型直接量，八进制直接量（0-），十六进制直接量（0x-)，浮点型直接量   

出现场景：

- `1026`
- `3.14`
- `1.2e5`
- `0x10`

#### Boolean

值：true, false    

出现场景：

- 条件语句导致的系统执行的隐式类型转换 `if(隐式转换){}`
- 字面量或变量定义 `var bool = true;`

```javascript
/* 隐式转换 */
if(document.getElementById('not-exist-element')){
    //
}else{
    //执行这里的代码
}
```

#### Object

值：属性集合（用大括号以键值对方式）    

出现场景：

- `var obj = {name: 'Xinyang'};`

#### 变量转换表

不同变量之间某些时候会进行隐式转换，其转换规则如下：

|Value|Boolean|Number|String|
|-----|-------|------|------|
|undefined|false|NaN|"undefined"|
|null|false|0|"null"|
|true|true|1|"true"|
|false|false|0|"false"|
|''|false|0|''|
|'123'|true|123|'123'|
|'1a'|true|NaN|'1a'|
|0|false|0|"0"|
|1|true|1|"1"|
|Infinity|true|Infinity|"Infinity"|
|NaN|false|NaN|'NaN'|
|{}|true|NaN|"[object Object]"|

### 对象类型

#### 内置对象类型(9个)

内置对象，其实也叫内置构造器，它们可以通过new方式创建一个新的对象。内置对象所属的类型就叫内置对象类型。

内置对象一共有9个，分别是：`Boolean` `String` `Number` `Object` `Array` `Date` `Error` `Function` `RegExp`（BSNO ADEFR）。其声明方式如下：

```javascript
var i = new String("str");    //String Object
var h = new Number(1);    //Number Object
var g = new Boolean(true);    //Boolean Object
var j = new Object({name : "Tom"}); //Object Object 
var k = new Array([1, 2, 3, 4]);    //Array Object
var l = new Date();    //Date Object
var m = new Error();
var n = new Function();    
var o = new RegExp("\\d");
```
要注意，虽然标准类型中有Boolean String Number Object，内置对象类型中也有Boolean String Number Object，但它们其实是通过不同的声明方式来进行区别的。标准类型通过直接赋值，而对象类型则是通过构造器实现初始化。

```javascript
var stdType = "hello";  //标准类型
var objType = new String("hello");  //对象类型
```

##### String

- 实例化方法

```
var str0 = 'ShuYi';
var str1 = new String('ShuYi');
```

- 属性及方法（相当于类的静态方法）

prototype、fromCharCode（转换 ASCII 代码为字符）

```javascript
var str0 = String.fromCharCode(83, 104, 117, 89, 105); //String "ShuYi"
```

- 原型对象属性及其方法（相当于父类的方法）

constructor、indexOf、replace、slice、split、charCodeAt、toLowerCase

**String.prototype.indexOf**

功能：获取子字符串在字符串中的索引

```
// stringObject.indexOf(searchValue, fromIndex)
var str = "I am X. From China!";
var index = str.indexOf('a'); // 2
str.indexOf('a', index + 1); // 16
str.indexOf('Stupid'); // -1 字符串不存在
```
**String.prototype.replace**

功能：查找字符串替换成目标文字

```
// stringObject.replace(regexp/substr, replacement)
var str = "apple is bad";
str = str.replace('bad', 'awesome');
```
**String.prototype.split**

功能：按分隔符将分隔符分成字符串数组

```
// stringObject.split(separator, arrayLength)
var str = '1 2 3 4';
str.split(' '); // ['1', '2', '3', '4'];
str.split(' ', 3); // ['1', '2', '3'];
str.split(/\d+/); // ["", " ", " ", " ", ""]
```

- 实例对象属性及方法（相当于实例化后才能调用的方法） 

无

##### Number

- 实例化方法

var num = new Number("10");

- 属性及方法（相当于类的静态方法）

prototype、MAX_VALUE、MIN_VALUE、NaN、NEGATIVE_INFINITY、POSITIVE_INFINITY   

```
var max = Number.MAX_VALUE;
var min = Number.MIN_VALUE;
```

- 原型对象属性及其方法（相当于父类的方法）

constructor、toFixed、toExponential...

```
var originalNum = 2.143;
fixNum = originalNum.toFixed(1);  
```

- 实例对象属性及方法（相当于实例化后才能调用的方法） 

无

##### Boolean 

- 实例化方法

`var flag = new Boolean("true");`

- 属性及方法（相当于类的静态方法）

prototype

- 原型对象属性及其方法（相当于父类的方法）

constructor、toString、valueOf...

- 实例对象属性及方法（相当于实例化后才能调用的方法） 

无

##### Object 

- 实例化方法
```
var obj0 = new Object({name: 'X', age: 13});
// 常用方法
var obj1 = {name: 'Q', age: 14};
```
- 属性及方法（相当于类的静态方法）

prototype、create、keys...


**Object.create**

功能：基于原型对象创造新对象(类似于继承)

```
// objectInstance.toString()
// Shape - superclass
function Shape() {
  this.x = 0;
  this.y = 0;
}
// superclass method
Shape.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
  console.info('Shape moved.');
};
// Rectangle - subclass
function Rectangle() {
  Shape.call(this); // call super constructor.
}
// subclass extends superclass
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;
var rect = new Rectangle();
console.log('Is rect an instance of Rectangle? ' + (rect instanceof Rectangle)); // true
console.log('Is rect an instance of Shape? ' + (rect instanceof Shape)); // true
rect.move(1, 1); // Outputs, 'Shape moved.'
```

- 原型对象属性及其方法（相当于父类的方法）

constructor、toString、valueOf、hasOwnProperty...

**Object.prototype.hasOwnProperty**

功能：判断一个属性是否是一个对象的自身属性

```
// objectInstance.hasOwnProperty("propertyName")
var obj = Object.create({a: 1, b: 2});
obj.c = 3;
obj.hasOwnProperty('a'); // false
obj.hasOwnProperty('c'); // true
```

- 实例对象属性及方法（相当于实例化后才能调用的方法） 

无

##### Array

- 实例化方法

var a2 = new Array(1, 'abc', true);

- 属性及方法（相当于类的静态方法）

prototype、isArray

```
var numArray = [2, 3, 4];
var isArray = Array.isArray(numArray);
```

- 原型对象属性及其方法（相当于父类的方法）

constructor、splice、forEach、find、concat、pop、push、reverse、shift、slice   

**Array.prototype.splice**

功能：从数组中删除或添加元素，返回被删除的元素列表（作用于原有数组）

`arrayObject.splice(start, deleteCount[, addedItem1[, addedItem2[, ...]]])`

```
var arr = ['1', '2', 'a', 'b', '6'];
var ret = arr.splice(2, 2, '3', '4', '5'); // ['a', 'b']
arr; // ['1', '2', '3', '4', 5', '6']
```
**Array.prototype.forEach**

功能：遍历元素组并调用回调函数

`arrayObject.forEach(callback[, thisArg])`

```
// 回调函数
// function callback(value, index, arrayObject) {...}
// value - 当前值 index - 当前索引 arrayObject - 数组本身
function logArray(value, index, arrayObject) {
	console.log(value);
	console.log(value === arrayObject[index]);
	}
//自动忽略空值 
//输出：2 true 5 true 9 true
[2, 5,  , 9].forEach(logArray);
```

- 实例对象属性及方法（相当于实例化后才能调用的方法） 

length

```
var numArray = [2, 3, 4];
var numArrayObj = new Array(2, 3, 4, 5);
var numOfArray = numArray.length;
var numOfArrayObj = numArrayObj.length;
```

##### Date

- 实例化方法

var date0 = new Date();
var date1 = new Date(2014, 3, 1, 7, 1, 1, 100);

- 属性及方法（相当于类的静态方法）

prototype、parse 、now...

- 原型对象属性及其方法（相当于父类的方法）

constructor、Date、getDate、getHours、setDate、setHours...

- 实例对象属性及方法（相当于实例化后才能调用的方法） 

无

##### Error

- 实例化方法

new Error([message[, fileName[, lineNumber]]])

message：错误消息，可选

fileName：出现错误的文件，可选

lineNumber：错误代码所在行号

- 属性及方法（相当于类的静态方法）

prototype

- 原型对象属性及其方法（相当于父类的方法）

toSource()、toString()

- 实例对象属性及方法（相当于实例化后才能调用的方法） 

暂无

- 例子

**Example: Throwing a generic error**

```javascript
try {
  throw new Error('Whoops!');
} catch (e) {
  alert(e.name + ': ' + e.message);
}
```
**Example: Handling a specific error**

```
try {
  foo.bar();
} catch (e) {
  if (e instanceof EvalError) {
    alert(e.name + ': ' + e.message);
  } else if (e instanceof RangeError) {
    alert(e.name + ': ' + e.message);
  }
  // ... etc
}
```

**Example: Custom Error Types**

```
// Create a new object, that prototypally inherits from the Error constructor.
function MyError(message) {
  this.name = 'MyError';
  this.message = message || 'Default Message';
}
MyError.prototype = Object.create(Error.prototype);
MyError.prototype.constructor = MyError;

try {
  throw new MyError();
} catch (e) {
  console.log(e.name);     // 'MyError'
  console.log(e.message);  // 'Default Message'
}

try {
  throw new MyError('custom message');
} catch (e) {
  console.log(e.name);     // 'MyError'
  console.log(e.message);  // 'custom message'
}
```

##### Function

- 实例化方法
```
// 对象实例化
var f0 = new Function('i', 'j', 'return (i + j)');
// 函数关键字语句
function f1(i, j){return i + j;}
// 函数表达式
var f3 = function(i, j){return i + j;};
```

- 属性及方法（相当于类的静态方法）

prototype

- 原型对象属性及其方法（相当于父类的方法）

constructor、apply、call、bind

- 实例对象属性及方法（相当于实例化后才能调用的方法） 

length 实参个数
prototype
arguments
caller 调用者

- 例子 

**Function.prototype.apply**

功能：通过参数指定调用者和函数参数并执行该函数

```
// functionObj.apply(thisArg[, argsArray])
function Point(x, y) {
  this.x = x;
  this.y = y;
}
Point.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
}
var p = new Point(1, 1);
var circle = {x: 1, y: 1, r: 1};
//指定circle执行p.move方法
p.move.apply(circle, [2, 1]); // {x: 3, y: 2, r: 1}
```
**Function.prototype.bind**

功能：通过参数指定函数调用者和函数参数并返回该函数的引用

```
// functionObj.bind(thisArg[, arg1[, arg2[, ...]]])
function Point(x, y) {
  this.x = x;
  this.y = y;
}
Point.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
}
var p = new Point(1, 1);
var circle = {x: 1, y: 1, r: 1};
//让circleMoveRef绑定p.move()方法
var circleMoveRef = p.move.bind(circle, 2, 1);
setTimeout(circleMoveRef, 1000); // {x: 3, y: 2, r: 1}
/*去掉setTimeout(...)语句而直接使用 circleMoveRef() 效果等同于 apply() */
/*circleMoveRef();*/
```

##### RegExp

- 实例化方法

`var regExp = new RegExp(/\d+/i); //i表示忽略大小写 `

- 属性及方法（相当于类的静态方法）

prototype

- 原型对象属性及其方法（相当于父类的方法）

constructor、test、exec、...

**RegExp.prototype.test**

功能：使用正则表达式对字符串进行测试，并返回测试结果

```
// regexObj.text(str)
var reg = /^abc/i;
reg.test('Abc123'); // true
reg.test('1Abc1234'); // false

- 实例对象属性及方法（相当于实例化后才能调用的方法） 

无

#### 普通对象类型

普通对象类型包括Math、JSON、全局对象三种。普通对象类型的特点就是其直接可以通过Math.method方式调用，类似于工具类一样，可以直接通过类调用静态方法。如：Math.random()返回一个0-1之间的随机数，JSON.parse(jsonStr)解析JSON字符串为JSON对象……

##### Math

- 对象说明

拥有属性和方法的单一对象主要用于数字计算

- 对象属性

E、PI、S、QRT2...

```
var piOfMath = Math.PI; //piOfMath = 3.141592653589793
```

- 对象方法

floor、random、abs、max、cos、ceil

**Math.floor**

功能：向下取整

```
// Math.floor(num)
Math.floor(0.97); // 0
Math.floor(5.1); // 5
Math.floor(-5.1); //6
相似方法：ceil，round
```

**Math.random**

功能：返回 0~1 之间的浮点数

```
// Math.random()
Math.random(); // 0.14523562323461
```

##### JSON

- 对象说明

用于存储和交换文本信息

- 对象方法

parse
stringify

**JSON.stringify**

功能：将 JSON 对象转换为字符转

`JSON.stringify(value[, replacer[, space]])`

```
var json = {'name': 'X'};
JSON.stringify(json); // "{"name":"X"}"
```

**JSON.parse**

功能：将 JSON 字符转转换为对象

`JSON.parse(text[, reviver])`

```
var jsonStr = '{"name":"X"}';
JSON.parse(jsonStr); // {name: 'X'}
var nameStr = jsonObj["name"]; // X
```

##### 全局对象

全局对象定义了一系列的属性和方法在编程过程中可以被之间调用。

- 属性

NaN、Infinity、undefined

- 方法

parseInt、parseFloat、isNaN、isFinite、eval……

**处理 URI 方法**

encodedURIComponent
decodeURIComponent
encodedURI
decodeURI

#### 自定义对象类型

自定义对象类型就是自己定义的对象，可以理解成Java中的类。

```javascript
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
}

var p = new Point(1, 2);
```

上面代码声明一个Point对象，并为Point对象增加了一个move方法，最后创建了一个Point对象。
