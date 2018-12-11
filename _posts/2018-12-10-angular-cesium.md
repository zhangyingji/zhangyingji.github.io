---
layout:     post
title:      "Angular配置Cesium"
subtitle:   ""
date:       2018-12-11 20:28:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

## 前言

环境：
- Angular: 7.1.2
- Cesium: 1.52

参考来源:
1. https://blog.csdn.net/5hongbing/article/details/78194267?utm_source=blogxgwz2
2. https://cesium.com/blog/2018/03/12/cesium-and-angular/
3. https://543802360.github.io/2017/08/26/%E4%BD%BF%E7%94%A8Angular%E5%BC%80%E5%8F%91Cesium/

## 配置cesium

```
# 安装cesium
npm install --save cesium
```

修改angular.json，全局引入

```
"assets": [ // ...
  { "glob": "**/*", "input": "./node_modules/cesium/Build/Cesium", "output": "./assets/cesium" }
 ],
"styles": [ // ...
  "./node_modules/cesium/Build/Cesium/Widgets/widgets.css"
],
"scripts": [ // ...
  "./node_modules/cesium/Build/Cesium/Cesium.js"
],
```

main.ts添加以下代码，引导浏览器加载cesium的各种资源文件

```
window['CESIUM_BASE_URL'] = '/assets/cesium';
```

新建组件

```
ng generate component cesium
```

在cesium.component.html中加入cesium容器

```
<div id="cesiumContainer"></div>
```

在cesium.component.ts中加入cesium的js代码

```
ngOnInit() {
var viewer = new Cesium.Viewer('cesiumContainer');
}
```

在APP下增加typing.d.ts文件,增加对Cesium对象全局声明

```
declare var Cesium: any;
```


在app.component.html加载cesium组件

```
<app-cesium></app-cesium>
```

在style.css中加入全局样式

```
html, body, #cesiumContainer {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
    overflow: hidden;
}

```