---
layout:     post
title:      "exports和module.exports"
subtitle:   ""
date:       2019-03-18 15:27:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

# 写在前面

官网是这么建议的，如果你怕混淆，只用`module.exports`就好了。

# 要点

1. `exports`是指向的`module.exports`的引用
2. module.exports初始值为一个空对象{}，故exports也为{}

知道`exports`是`module.exports`的引用，则可知
- 当`exports`被完全替换时，则不再指向`module.exports`
- 当`module.exports`被完全替换时，`exports`不会改变

```javascript
console.log(module.exports === exports) // 初始化 true 

exports = module.exports // 让 exports 重新指向 module.exports
```

# 进一步

值得注意的是：`require()`返回`module.exports`

```javascript
module.exports.hello = true; // 被导出
exports = { hello: false };  // 没有被导出
```

这种情况可以通过模拟`require`说明

```javascript
function require() {
  const module = {
    exports: {}
  };
  
  // 修改exports只在内部起作用，无法影响到外部module.exports
  ((module, exports) => {
    // Module code here. In this example, define a function.
    function someFunc() {}
    exports = someFunc;
    // At this point, exports is no longer a shortcut to module.exports, and
    // this module will still export an empty default object.
    module.exports = someFunc;
    // At this point, the module will now export someFunc, instead of the
    // default object.
  })(module, module.exports);
  
  return module.exports;
}
```
