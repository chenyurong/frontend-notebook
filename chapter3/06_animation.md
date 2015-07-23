<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [JavaScript 动画](#javascript-%E5%8A%A8%E7%94%BB)
  - [JavaScript 动画三要素](#javascript-%E5%8A%A8%E7%94%BB%E4%B8%89%E8%A6%81%E7%B4%A0)
    - [定时器](#%E5%AE%9A%E6%97%B6%E5%99%A8)
      - [setInterval](#setinterval)
      - [setTimeout](#settimeout)
      - [requestAnimationFrame](#requestanimationframe)
  - [JavaScript 动画DEMO](#javascript-%E5%8A%A8%E7%94%BBdemo)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## JavaScript 动画

**帧**，为动画的最小单位，一个静态的图像。**帧频**，每秒播放的帧的数量。一个动画是由很多帧组成的，因为人眼的暂留特性，当图片交替的速度大于每秒 30 帧就会有动画的感觉。

**实现方式**

- gif 图像形式存储，容量大，需第三方制图工具制作。
- flash 需要第三方制作工具，不推荐。
- CSS3 实现动画具有局限性
- JavaScript 可实现大部分上面几类可实现的动画效果

### JavaScript 动画三要素

![](../img/J/javascript-animation.jpg)

#### 定时器

##### setInterval

```javascript
var intervalId = setInterval(func, delay[, param1, param2, ...]);
//clearInterval(intervalId); //清除定时器
```

- `func` 执行改变属性操作函数
- `delay` 触发的时间间隔（毫秒为单位）
- `param1, param2, ...` 为执行时可传入改变属性函数的参数，可选。

NOTE：使用 `setInterval` 可以调用一次定时器既可实现连贯的动画，但最后需要使用 `clearInterval` 即可清除动画效果。

##### setTimeout

```javascript
var timeoutId = setTimeout(func[, delay, param1, param2, ...]);
//clearTimeout(timeoutId); //清除定时器
```

- `func` 为执行改变属性的操作
- `delay` 为出发时间间隔（毫秒为单位）默认为 0，可选。
- `para1` 为执行时可传入改变属性函数的参数，可选。

NOTE：使用 `setTimeout` 实现动画，则需要在动画每一帧结束时再次调用定时器，但它无需清除定时器。

**区别**

- `setTimeout` 在延时后只执行一次，`setInterval` 则会每隔一个延时期间后会再执行。

##### requestAnimationFrame

类似于 `setTimeout` 但是无需设定时间间隔。此定时器为 HTML5 中的新标准，其间隔时间不由用户控制，而是由显示器的刷新频率决定。（市面上的显示器刷新频率为每秒刷新60次）

```javascript
var requestId = requestAnimationFrame(func);
cancelAnimationFrame(requestId);
```

NOTE：使用它来实现动画与 `setTimeout` 类似，需要每次每帧结束时再次调用，但它无需清除定时器。不可设置时间间隔（系统决定），时间间隔为16.67毫秒一帧。

**优势**

- 无需设置间隔时间
- 动画流畅度高

### JavaScript 动画DEMO

**常见动画**

大多的复杂动画都是有下列的简单动画所组成的。

- 形变，改变元素的宽高
- 位移，改变元素相对位置
- 旋转
- 透明度
- 其他...

下面的例子为以 px 为单位的动画代码

```javascript
var animation = function(ele, attr, from, to) {
  var distance = Math.abs(to - from);
  var stepLength = distance/100;
  var sign = (to - from)/distance;
  var offset = 0;
  var step = function(){
    var tmpOffset = offset + stepLength;
    if (tmpOffset < distance) {
      ele.style[attr] = from + tmpOffset * sign + 'px';
      offset = tmpOffset;
    } else {
      ele.style[attr] = to + 'px';
      clearInterval(intervalID);
    }
  }
  ele.style[attr] = from + 'px';
  var intervalID = setInterval(step, 10);
}
```

