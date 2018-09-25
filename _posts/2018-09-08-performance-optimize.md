---
layout:     post
title:      "前端性能优化"
subtitle:   ""
date:       2018-09-08 21:32:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 前端
---

## 基础

- 减少DOM操作
- CSS放头部：减少首页加载时间
- JS放底部：减少首页加载时间
- 使用CDN

## 减少http请求

- 合并图片（CSS sprites）
- 合并CSS、JS文件
- lazyLoad

## 压缩图片、CSS、JS文件

## 减少reflow(回流)和repaint(重绘)

`reflow`：例如某个子元素样式发生改变，直接影响到了其父元素以及往上追溯很多祖先元素（包括兄弟元素），这个时候浏览器要重新去渲染这个子元素相关联的所有元素的过程称为回流。

`repaint`：如果只是改变某个元素的背景色、文 字颜色、边框颜色等等不影响它周围或内部布局的属性，将只会引起浏览器 repaint（重绘）。repaint 的速度明显快于 reflow

以下操作会导致reflow:
1. 改变窗口大小
2. 改变文字大小
3. 内容的改变，如用户在输入框中敲字
4. 激活伪类，如:hover
5. 操作class属性
6. 脚本操作DOM
7. 计算offsetWidth和offsetHeight
8. 设置style属性

减少reflow的方法:
1. 不要通过父级来改变子元素样式，最好直接改变子元素样式，改变子元素样式尽可能不要影响父元素和兄弟元素的大小和尺寸
2. 尽量通过class来设计元素样式，切忌用style
3. 实现元素的动画，对于经常要进行回流的组件，要抽离出来，它的position属性应当设为fixed或absolute
4. 权衡速度的平滑。比如实现一个动画，以1个像素为单位移动这样最平滑，但reflow就会过于频繁，CPU很快就会被完全占用。如果以3个像素为单位移动就会好很多。
5. 不要用tables布局。tables中某个元素一旦触发reflow就会导致table里所有的其它元素reflow。
6. 在适合用table的场合，可以设置table-layout为auto或fixed，这样可以让table一行一行的渲染，这种做法也是为了限制reflow的影响范围。
7. css里不要有表达式expression
8. 减少不必要的 DOM 层级（DOM depth）。改变 DOM 树中的一级会导致所有层级的改变，上至根部，下至被改变节点的子节点。这导致大量时间耗费在执行 reflow 上面。
9. 避免不必要的复杂的 CSS 选择器，尤其是后代选择器（descendant selectors），因为为了匹配选择器将耗费更多的 CPU。
10. 尽量不要过多的频繁的去增加，修改，删除元素，因为这可能会频繁的导致页面reflow，可以先把该dom节点抽离到内存中进行复杂的操作然后再display到页面上。
11. 请求如下值offsetTop, offsetLeft, offsetWidth, offsetHeight，scrollTop/Left/Width/Height，clientTop/Left/Width/Height，浏览器会发生reflow，建议将他们合并到一起操作

## 优化检测

工具有chrome的两款插件：lighthouse和pagespeed