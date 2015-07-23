<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [切图技巧](#%E5%88%87%E5%9B%BE%E6%8A%80%E5%B7%A7)
  - [隐藏文字](#%E9%9A%90%E8%97%8F%E6%96%87%E5%AD%97)
  - [PNG24切图方法](#png24%E5%88%87%E5%9B%BE%E6%96%B9%E6%B3%95)
  - [PNG8带背景切图方法](#png8%E5%B8%A6%E8%83%8C%E6%99%AF%E5%88%87%E5%9B%BE%E6%96%B9%E6%B3%95)
  - [可平铺背景的切图方法](#%E5%8F%AF%E5%B9%B3%E9%93%BA%E8%83%8C%E6%99%AF%E7%9A%84%E5%88%87%E5%9B%BE%E6%96%B9%E6%B3%95)
  - [切片工具](#%E5%88%87%E7%89%87%E5%B7%A5%E5%85%B7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 切图技巧

- **内容性图片** 指的是图片在页面是作为内容存在，如页面中的海报。
- **修饰性图片** 指的是图片在页面中起修饰作用，如页面中的背景和图标。

#### 隐藏文字

- 方法一，直接在图层中隐藏文字图层
- 方法二（两种，分别应对于纯色和有背景需要隐藏文本的情况）如下图所示，使用自由变换。

#### PNG24切图方法

- 移动工具选中所需图层（<kbd>Ctrl</kbd> 多选）
- 右键合并图层（<kbd>Ctrl</kbd> + <kbd>E</kbd>）
- 复制到新图层

#### PNG8带背景切图方法

- 合并可见图层（<kbd>Shift</kbd> + <kbd>Ctrl</kbd> + <kbd>E</kbd>）
- 矩形选框选择内容
- 魔棒工具去除多余部分（<kbd>Alt</kbd> + 选取）

#### 可平铺背景的切图方法

- 用矩形选择一个区域
- 复制至新图层

NOTE: X 轴平铺需要占满图片的宽，Y 轴平铺需要占满图片的高。

#### 切片工具

大图化小的方法，将一大图分为多小图    

- 拉参考线
- 选择切片工具
- 点击 “基于参考线的切片” 按钮
- 选择切片选择工具
- 保存于新图层