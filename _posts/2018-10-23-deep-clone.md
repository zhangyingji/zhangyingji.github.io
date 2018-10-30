---
layout:     post
title:      "JS深拷贝"
subtitle:   ""
date:       2018-10-23 11:04:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

## 浅拷贝与深拷贝

浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存。但深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象。

## 深拷贝实现

1 一层拷贝用 Object.assign()函数

```
var obj1 = { a: 10, b: 20, c: 30 };
var obj2 = Object.assign({}, obj1);
obj2.b = 100;
console.log(obj1);
```

2 用JSON对象的stringify和parse方法

```
function deepClone(obj){
    let _obj = JSON.stringify(obj),
        objClone = JSON.parse(_obj);
    return objClone
}

let a = [0,1,[2,3],4],
    b = deepClone(a);
a[0] = 1;
a[2][0] = 1;
console.log(a,b);
```

3 用JQ的extend方法

$.extend( [true, ]target, object1 [, objectN ] )

```
let a=[0,1,[2,3],4],
    b=$.extend(true,[],a);
a[0]=1;
a[2][0]=1;
console.log(a,b);
```

4 递归

```
function deepClone(obj){
    let objClone = Array.isArray(obj) ? [] : {};
    if(obj && typeof obj === "object" {
        for(key in obj){
            if(obj.hasOwnProperty(key)) {
                // 判断ojb子元素是否为对象，如果是，递归复制
                if(obj[key] && typeof obj[key] === "object") {
                    objClone[key] = deepClone(obj[key]);
                } else {
                    // 如果不是，简单复制
                    objClone[key] = obj[key];
                }
            }
        }
    }
    return objClone;
}    

let a = [1,2,3,4],
    b = deepClone(a);
a[0] = 2;
console.log(a,b);
```

5 使用Object.create()方法

```
function deepClone(initalObj, finalObj) {    
  var obj = finalObj || {};    
  for (var i in initalObj) {
    // 避免相互引用对象导致死循环，如initalObj.a = initalObj的情况
    var prop = initalObj[i];        
    if(prop === obj) {            
      continue;
    }     
    
    if (typeof prop === 'object') {
      obj[i] = (prop.constructor === Array) ? [] : Object.create(prop);
    } else {
      obj[i] = prop;
    }
  }    
  return obj;
}
```
