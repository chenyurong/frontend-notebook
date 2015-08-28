# BOM中常用坐标类属性总结

js中获取各种宽度和距离，常常让我们混淆，各种浏览器的不兼容让我们很头疼，现在就在说说js中有哪些宽度和距离。	

## 名词解释

> - screen：屏幕。这一类取到的是关于屏幕的宽度和距离，与浏览器无关，应该是获取window对象的属性。
- client：使用区、客户区。指的是客户区，当然是指浏览器区域。
- offset：偏移。指的是目标甲相对目标乙的距离。
- scroll：卷轴、卷动。指的是包含滚动条的的属性。
- inner：内部。指的是内部部分，不含滚动条。
- avail：可用的。可用区域，不含滚动条，易与inner混淆。

## window

|属性|解释|兼容|推荐使用|
|:---:|:---:|:---:|:---:|
|window.innerWidth/innerHeight|浏览器可见区域宽高（包含滚动条，不包含边框）|ie9/10、chrome、firefox|-|
|window.outerWidth/outerHeight|浏览器可见区域宽高（包含滚动条和边框）|ie9/10、chrome、firefox|-|
|-|-|-|
|window.screenLeft/screenTop|浏览器内边距距离屏幕边缘的距离|ie6/7/8/9/10、chrome|√|
|window.screenX/screenY|浏览器外边距距离屏幕边缘的距离|ie9/10、chrome、firefox|×|
|-|-|-|-|
|window.pageXOffset/pageYOffset|表示浏览器X轴（水平）、Y轴（垂直）滚动条的偏移距离|ie9/10、chrome、firefox|√|
|window.scrollX/scrollY|表示浏览器X轴（水平）、Y轴（垂直）滚动条的偏移距离|chrome、firefox|×|

### window.innerWidth/innerHeight

描述：浏览器可见区域的内宽度、高度（不含浏览器的边框，但包含滚动条）。

兼容：ie9/10、chrome、firefox。

示例（缩放浏览器的宽度为1000px，高度为500px）：

```
alert(window.innerWidth); // chrome/firefox/ie9/10=>1000 // ie6/7/8=>undefined alert(window.innerHeight); // chrome/firefox/ie9/10=>500 // ie6/7/8=>undefined
```

### window.outerWidth/outerHeight

描述：浏览器外宽度（包含浏览器的边框，因各个浏览器的边框边一样，得到的值也是不一样的）。

兼容：ie9/10、chrome、firefox。

示例（缩放浏览器的宽度为1000px，高度为500px）：

```
alert(window.outerWidth); // chrome/firefox/ie9/10=>1002 // ie6/7/8=>undefined alert(window.outerHeight); // chrome/firefox/ie9/10=>502 // ie6/7/8=>undefined
```

NOTE：注意：没有window.width属性。

### window.screenLeft/screenTop

描述：浏览器的位移，表示：

> - ie浏览器的内边缘距离屏幕边缘的距离。
- chrome浏览器的外边缘距离屏幕边缘的距离。

兼容：ie6/7/8/9/10、chrome。

```
alert(window.screenLeft);
// ie=>87
// chrome=>86
// firefox=>undefined
alert(window.screenTop);
// ie=>87
// chrome=>86
// firefox=>undefined
```

### window.screenX/screenY

描述：浏览器的位移，表示：

> - ie9/10浏览器的外边缘距离屏幕边缘的距离。
- chrome浏览器的外边缘距离屏幕边缘的距离。

由此可知，chrome的screenLeft和screenX是相等的（其目的是为了兼容ie和firefox，两个属性都兼备了，但更趋向于firefox，chrome的这种做法不止这一处，还有很多，其实这种做法便于开发者移植，但对开发者的开发过程产生了一定的混淆），ie9/10的screenLeft是大于screenX的，如图：

兼容：ie9/10、chrome、firefox。

```
alert(window.screenX);
// chrome/firefox=>86
// ie9/10=>79
// ie6/7/8=>undefined
alert(window.screenY);
// chrome/firefox=>86
// ie9/10=>79
// ie6/7/8=>undefined
```

### window.pageXOffset/pageYOffset

描述：表示浏览器X轴（水平）、Y轴（垂直）滚动条的偏移距离。

兼容：ie9/10、chrome、firefox。

示例：

```
document.onclick=function(){
alert(window.pageXOffset);
// chrome=>200
// firefox=>200
// ie9/10=>200
// ie6/7/8=>undefined
alert(window.pageYOffset);
// chrome=>200
// firefox=>200
// ie9/10=>200
// ie6/7/8=>undefined
};
```

### window.scrollX/scrollY

描述：表示浏览器X轴（水平）、Y轴（垂直）滚动条的偏移距离。由此可知，在chrome和firefox中window.pageXOffset和window.scrollX是相等的，具体为什么会出现两个相等的属性值，不得而知。

兼容：chrome、firefox。

示例：

```
document.onclick=function(){
	alert(window.scrollX);
	// chrome=>200
	// firefox=>200
	// ie6/7/8/9/10=>undefined

	alert(window.scrollY);
	// chrome=>200
	// firefox=>200
	// ie6/7/8/9/10=>undefined
};
```

## screen

### screen.width/height

描述：屏幕的宽度、高度（指的是屏幕的分辨率，单位为像素）。

兼容性：ie6/7/8/9/10、chrome、firefox。

示例（屏幕的分辨率为1440×900）：

```
alert(screen.width);
// chrome/firefox/ie6/7/8/9/10=>1440
alert(screen.height);
// chrome/firefox/ie6/7/8/9/10=>900
```

注意：此处必须是screen.width，而不是screenWidth，与接下来要说的各种宽度有所区别。

### screen.availWidth/availHeight

描述：屏幕的可用宽度、高度（通常与屏幕的宽度、高度一致）。

兼容性：ie6/7/8/9/10、chrome、firefox。

示例：

```
alert(screen.availWidth);
// chrome/firefox/ie6/7/8/9/10=>1440
alert(screen.availHeight);
// chrome/firefox/ie6/7/8/9/10=>900
```

### element

元素的宽度、位移、距离以元素的盒模型为content-box为例。即：

box-sizing: content-box;
其他盒模型计算会有差异，请勿对号入座。

### elment.clientWidth/clientHeight

描述：计算如下，

有滚动条时：clientWidth=元素左内边距宽度+元素宽度+元素右内边距宽度-元素垂直滚动条宽度
无滚动条时：clientWidth=元素左内边距宽度+元素宽度+元素右内边距宽度
使用该特性可以计算出的滚动条宽度（即设置元素的内容宽度超过元素宽度，然后分别设置是否超过隐藏，两次的clientWidth差值就是滚动条的宽度）。

兼容：chrome、firefox、ie6/7/8/9/10。

示例（宽度和高度都为100px，边框为50px，内边距为60px，外边距为70px，左、上位移为80px，滚动条的宽度因系统不同而不同）：

```
// 有滚动条=>paddingLeftWidth+width+paddingRightWidth-scrollYWidth
// 无滚动条=>paddingLeftWidth+width+paddingRightWidth
alert(oDemo.clientWidth);
// 有滚动条=>60+100+60-17=203
// 无滚动条=>60+100+60=220
 
// 有滚动条=>paddingTopWidth+height+paddingBottomWidth-scrollYHeight
// 无滚动条=>paddingTopWidth+height+paddingBottomWidth
alert(oDemo.clientHeight);
// 有滚动条=>60+100+60-17=203
// 无滚动条=>60+100+60=220
```

### element.clientLeft/clientTop

描述：clientLeft为左边框宽度，clientTop为上边框宽度。

兼容：chrome、firefox、ie6/7/8/9/10。

示例（宽度和高度都为100px，边框为50px，内边距为60px，外边距为70px，左、上位移为80px，滚动条的宽度因系统不同而不同）：

```
// borderLeftWidth
alert(oDemo.clientLeft);
// =>50
 
// borderTopWidth
alert(oDemo.clientTop);
// =>50
```

### element.offsetWidth/offsetHeight

描述：offsetWidth=元素左边框宽度+元素左内边距宽度+元素宽度+元素右内边距宽度+元素右边框宽度。

兼容：chrome、firefox、ie6/7/8/9/10。

示例（宽度和高度都为100px，边框为50px，内边距为60px，外边距为70px，左、上位移为80px，滚动条的宽度因系统不同而不同）：

```
// borderLeftWidth+paddingLeftWidth+width+paddingRightWidth+borderRightWidth
alert(oDemo.offsetWidth);
// =>50+60+100+60+50=320
 
// borderTopWidth+paddingLeftWidth+width+paddingRightWidth+borderRightWidth
alert(oDemo.offsetWidth);
// =>50+60+100+60+50=320
```

### element.offsetLeft/offsetTop

描述：表示该元素相对于最近的定位祖先元素的距离，

chrome：offsetLeft=定位祖先左边框宽度+定位祖先元素左内边距宽度+左位移+左外边距宽度

ie6/7/8/9/10、firefox：offsetLeft=定位祖先元素左内边距宽度+左位移+左外边距宽度。

chrome比其他浏览器多计算了定位祖先元素的边框。offsetTop同理。

兼容：chrome、firefox、ie6/7/8/9/10。

示例（宽度和高度都为100px，边框为50px，内边距为60px，外边距为70px，左、上位移为80px，滚动条的宽度因系统不同而不同）：

```
// 以最近的定位祖先元素为准
// 谷歌=>parentBorderLeftWidth+parentPaddingLeftWidth+left+marginLeft
// 其他=>parentPaddingLeftWidth+left+marginLeft
alert(oDemo.offsetLeft);
// chrome=>20+10+80+70=180
// ie6/7/8/9/10/firefox=>160
 
// 以最近的定位祖先元素为准
// 谷歌=>parentBorderTopWidth+parentPaddingTopWidth+left+marginLeft
// 其他=>parentBorderTopWidth+left+marginLeft
alert(oDemo.offsetLeft);
// chrome=>20+10+80+70=180
// ie6/7/8/9/10/firefox=>160
```

### element.scrollWidth/scrollHeight

描述：计算方法如，

有滚动条时：
chrome、firefox、ie8/9/10：左内边距宽度+内容宽度。
ie6/7：左内边距宽度+内容宽度+右内边距宽度（是由CSS的BUG引起）。
无滚动条时：左内边距宽度+宽度+右内边距宽度。
兼容：chrome、firefox、ie8/9/10、ie6/7（半兼容）。

示例（宽度和高度都为100px，边框为50px，内边距为60px，外边距为70px，左、上位移为80px，滚动条的宽度因系统不同而不同，内容宽度和高度都为200px）：

```
// 有滚动条=paddingLeftWidth+contentWidth
// 有滚动条(ie6/7)=paddingLeftWidth+contentWidth+paddingRightWidth
// 无滚动条=paddingLeftWidth+width+paddingRightWidth
alert(oDemo.scrollWidth);
// 有滚动条=>200+60=260
// 有滚动条(ie6/7)=>200+60+60=320
// 无滚动条=>100+60+60=220
 
// 有滚动条=paddingTopWidth+contentWidth
// 有滚动条(ie6/7)=paddingTopWidth+contentWidth+paddingBottomWidth
// 无滚动条=paddingTopWidth+width+paddingBottomWidth
alert(oDemo.scrollHeight);
// 有滚动条=>60+200=260
// 有滚动条(ie6/7)=>60+200+60=320
// 无滚动条=>60+100+60=220
```

### element.scrollLeft/scrollTop

描述：获得水平、垂直滚动条的距离。

兼容：chrome、firefox、ie6/7/8/9/10。

示例（宽度和高度都为100px，边框为50px，内边距为60px，外边距为70px，左、上位移为80px，滚动条的宽度因系统不同而不同）：

```
document.onclick=function(){
	// 水平滚动条左距离
	alert(oDemo.scrollLeft);
 
	// 垂直滚动条上距离
	alert(oDemo.scrollTop);
}
```




