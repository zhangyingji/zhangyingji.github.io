---
layout:     post
title:      "JavaScript高级程序设计"
subtitle:   "第3版 学习笔记"
date:       2018-08-19 16:42:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
---

## 1 组成

- ECMAScript
- 文档对象模型(DOM,Document Object Model)
- 浏览器对象模型(BOM,Browser Object Model)

## 2 使用JS

noscript标签：脚本不能执行时显示此部分
 
延迟脚本

```
// 页面解析完后运行，只适用外部脚本，且不一定按顺序执行
defer=“defer”
```

异步脚本
```
// 需要确保脚本不存在依赖关系
stript async
```

## 3 基本概念

标识符 驼峰表示法

注释 //  /**/

严格模式

```
“use strict”;
```

变量
```
var message = "hi";
```

##### 基本数据类型

Undefined

声明而未初始化时

Null

Boolean

Number

```
// 检测“不是数值”
isNaN(); 

// 数值转换
parseInt();
parseFloat();
Number(); // 复杂
```


String

```
// 转换为字符串
var ageAsString = age.toString();
// 字符串拼接
var lang = "Java" + "Script";
```


Object

检测类型： typeof

##### 操作符

```
++ --
~ NOT
& AND
| OR
^ XOR
<< 左移
\>> 有符号右移; >>> 无符号右移
&& || ! 与或非
\* % + -
< > <= >= 
== != === !===
?: = ,
```

##### 语句


if

do-while

while

for

for-in

迭代对象为null或undefinded时会抛出错误


label && break && continue

with

严格模式下不允许使用，大量使用会导致性能下降

switch

```
switch(expression) {
    case value: statement
        break;
    default;
}
```

##### 函数

function

```
// 不能重载，但是可通过arguments对象访问参数数组，判断arguments.length达到伪重载
function functionName(arg0,...,argN) {
    statements
}

```

## 4 变量、作用域和内存
##### 基本类型和引用类型的值

复制引用类型的值→引用的是同一个对象

传递函数：参数都是按值传递的

检测类型：基本数据类型用 typeof

```
// 对象或者null则返回object
```

对象类型用 instanceof

```
// 引用类型、Object构造函数为true,基本类型则返回false
alert(person instanceof Object)
```

##### 执行环境及作用域

延长作用域链：catch块、with语句

没有块级作用域：if、for语句声明的变量会存在于外部执行环境中

声明变量：使用var声明的变量会被添加到最接近的环境中，如函数内最接近的环境为该函数的局部环境；若不使用var，则添加至全局环境

查询标识符

```
// 向上逐级查询，匹配即停止
var color = "blue";

function getColor(){
    var color = "red";
    return color;
}

alert(getColor()); // "red"
```

##### 垃圾收集

机制：找出不再使用的变量，释放其占用的内存

一般函数执行结束，则可以释放局部变量占的内存

标记清除（主流）：标识进入环境、离开环境

引用计数（存在循环引用的问题）

性能问题？

管理内存

优化内存占用：只保存必要的数据。一旦数据不再有用，解除引用（置null），这样垃圾收集器下次运行时则会将其回收

## 5 引用类型
##### Object类型

创建

```
// 1 new
var person = new Object();
person.name = "Zhang Yingji";
// 2 对象字面量，可读性好
var person = {
    name : "Zhang Yingji";
}
```

对象字面量是向函数传递大量可选参数的首选方式

访问对象属性使用点表示法

##### Array类型

创建

```
// 1 new
// new可省略
var colors = new Array();
var colors = new Array(20);
var colors = new Array("red","blue","green");
// 2 数组字面量
var colors = ["red","blue","green"];
var names = [];
```

length属性

检测数组

```
// 一个网页/全局作用域/框架
if (value instanceof Array) {
    // do something
}
// 通用情况,IE9+
if {Array.isArray(value) {
    // do something
}
```

转换方法 toLocaleString();tostring();valueOf()

栈方法 push();pop()

队列方法 push();shift()

重排序方法 reverse();sort()

```
// sort()会转化为字符串后再比较
// 故接受一个比较函数来正确排序
function compare(value1,value2) {
    if(value1 < value2) {
        return -1;
    } else if (value > value2) {
        return 1;
    } else {
        return 0;
    }
}

values.sort(compare);
```

操作方法

```
// concat() 创建新的数组，末尾追加
var colors2 = colors.concat("yellow");

// slice(start,[end]) 创建新的数组，返回索引start到end的项，不包括end
var colors3 = colors.slice(2);

// splice()
// 删除，指定起始位置、要删除的项数
splice(0,2)
// 插入，指定起始位置、要删除的项数、要插入的项
splice(2,0,"zhang","yingji");
// 替换，指定起始位置，要删除的项数，要插入的项
splice(2,1,"zhang");
```

位置方法

接收的参数：要查找项和表示查找起点的索引（可选）

```
// 从开头向后查找
indexOf()
// 从结尾向前查找
lastIndexOf()
```

迭代方法...

归并方法...

##### Date 类型
```
// 创建,获得当前日期和时间
var now = new Date();

// 基于GTM创建指定日期 
// 1 Date.parse(),可以后台调用
var someDate = new Date("May 25,2004");
// 2 Date.UTC()
// GMT 2005.5.5 5:55:55,一月是0
var allFives = new Date(Date.UTC(2005,4,5,17,5,5)

// 基于系统设置本地时区，参数一致
var allFives = new Date(2005,4,5,17,5,5)

// 返回调用方法时的毫秒数
var start = Date.now();
```

继承的方法/格式化方法

日期/时间组件方法 P102

##### RegExp类型

创建

```
// 使用字面量形式
var expression = / pattern / falgs

// 使用构造函数
var pattern = new RegExp("pattern","flags")
```

flgs可有一或多个：
1. g 被应用于所有字符串
2. i 不区分大小写
3. m 到达一行末尾时还会继续查找下一行

正则表达式元字符需要转义：

```
([{\^$|)>*+.]}
```

RegExp实例属性、方法

```
// exec()
// test()，验证是否匹配时常用
if(pattern.test(text)) {
    alert("matched")
}
```

RegExp构造函数属性、模式局限性...

##### Function类型

声明

```
// 函数声明，提前
function sum(num1,num2){}

// 函数表达式,另外构造函数法不推荐
var sum = function(num1,num2){}
```

没有重载

作为值的函数

函数内部属性：arguments,this

```
// arguments.callee解除代码与函数名的耦合
// 现在已不推荐使用,因为每次递归调用时都需要重新创建。影响浏览器的性能，还会影响闭包
function factorial(num) {
    if(num <= 1) {
        return 1;
    } else {
        return num * arguments.callee(num-1);
    }
}

// 改进的方法是给内部函数一个名字
```

函数属性和方法

1. 属性有 length 和 prototype
2. 方法有 `apply()`， `call()`,实际作用是设置函数体内this对象的值，区别在于接收参数的方式不同；强大之处在于扩充函数的作用域,对象和方法不需要有耦合关系；立即执行
```
// apply()接收的参数：一个是在其中运行函数的作用域，另一个是参数数组

// call()接收的参数：第一个是在其中运行函数的作用域，其余的是要传递的参数

window.color = "red";
var o = { color: "blue"};

funciton sayColor(){
    alert(this.color);
}

sayColor();     //red

sayColor.call(this);    //red
sayColor.call(window);    //red
sayColor.call(o);    //blue

// bind()
```

3. `bind()` 创建一个函数实例,便于稍后调用

```
window.color = "red";
var o = {color: "blue";}

function sayColor(){
    alert("this.color");
}

var objectSayColor = sayColor.bind(o);
objectSayColor(); // blue
```

##### 基本包装类型

...

## 6 面向对象的程序设计

##### 理解对象

`Object.defineProperty()`,IE9+
`Object.defineProperties()`,IE9+

可以修改默认属性的特性，用得少，但是**可以帮助理解JavaScript对象**。

1 数据属性

下面通过一个例子了解一下数据属性

```
var person = {};
Object.defineProperty(person,"name",{
    configurable: false; // 不能从对象中删除属性，一旦如此就无法设置为true了
    enumerable: false; // 不能for-in循环
    writable: false; // 设置成只读
    value: "zhangyingji"; // 默认undefined
});
```

2 访问器属性

包括`configurable`,`enumerable`以及一对函数`getter`和`setter`（非必须，默认undefined）

```
var book = {
    _year: 2018;
}

Object.defineProperty(book,"year",{
    get: function(){
        return this._year;
    },
    set: function(new){
        if(new>2018) {
            this._year = new;
        }
    }
});
```

3 读取属性的特性

`getOwnPropertyDescriptor()` ,IE9+

```
var discriptor = Object.getOwnPropertyDescriptor(book,"_year");
```

##### 创建对象

使用同一个接口创建很多对象，会产生大量重复代码

~~1 工厂模式~~

缺点：没有解决对象识别的问题

```
function createPerson(name){
    var o = new Object();
    o.name = name;
    return o;
}

var preson1 = createPerson("Tom");
```

2 构造函数模式

特点：构造函数大写字母开头，用new实例化

**缺点**：每个方法都在实例上重新创建

```
function Person(name){
    this.name = name;
}

var person1 = new Person("name");
```

3 原型模式

每个函数都有一个`prototype`属性，它是一个指针，指向一个对象(原型对象)。它包含可以由特定类型的所有实例共享的属性和方法。

**优点**：让所有对象实例共享它所包含的属性和方法

```
function Person(name){
    this.name = name;
}

Person.prototype.sayName = function(){
    alert("this.name");
}

var person1 = new Person("name");
```

**3.1 理解原型对象**

【函数与原型对象】创建新函数→得到prototype属性，指向原型对象→原型对象获得一个constructor(构造函数)属性，指向prototype所在的（构造）函数，举例:Person.protype.constructor指向Person

【实例与构造函数的原型对象】创建实例对象→内部包含一个指针[[Prototype]]，\_\_proto\_\_,指向构造函数的原型对象，举例：person1的[[Prototype]]指向Person的原型对象

确定这种关系的方法

```
// 原型对象方法 isPrototypeOf()
alert(Person.prototype.isPrototypeOf(person1)); // true

// Object.getPrototypeOf() 返回[[prototype]]的值，IE9+
alert(Object.getPrototypeOf(person1) == Person.protoye); // true
```

搜索属性时，从实例往原型对象向上搜，直到找到为止

使用`hasOwnProperty()`检测一个属性是否存在实例当中，存在返回true

```
alert(person1.hasOwnProperty('name'));
```

3.2 原型与 in 操作符

只要通过对象能访问到属性就返回true

结合`hasOwnProperty()`使用，在对象属性存在的情况下，**封装函数来判断属性存在实例中还是原型中**

```
// 在原型中返回ture
function hasPrototypeProperty(object,name){
    return !object.hasOwnproperty(name) && (name in object);
}
```

所有定义的属性都是可枚举的（IE9+)

3.3 更简单的原型语法

**使用字面量(相当于重写prototype)**,但constructor属性不再指向构造函数了，如果很需要constructor,则可以在字面量中加入constructor属性。

但只要它的[[Enumberable]默认设成了true,原生constructor是不可枚举的，可以使用Object.defineProperty()设为false

3.4 原型的动态性

**重写原型对象会切断现有原型与之前任何已经存在的对象实例之间的联系**

3.5 原生对象的原型

原生引用类型也是通过原型模式创建的

3.6 原型对象的问题

默认的初始化参数相同，包含引用类型值的属性会影响到所有实例

4 组合使用构造函数模式和原型模式

**优点**：实例有自己的属性副本，又共享了方法的引用，最大限度节省了内存

```
funcrion Person(name) {
    this.name = name;
    this.friends = ['xiaoming'];
}

Person.prototype = {
    constructor: Person,
    sayName: function(){
        alert(this.name);
    }
}
```

5 动态原型模式

**优点：把所有信息都封装在了构造函数中，通过判断存在的方法是否有效来决定是否要出书画原型，保持了组合使用的优点**。

if块初次调用构造函数才会执行，节省空间，若还要添加其他方法也可以直接写在if块中。因为要么它们全都还没有定义(new第一个实例时)，要么已经全都定义了(new其他实例后)，即它们的存在性是一致的，用同一个判断就可以了，而不需要分别对它们进行判断
    
```
function Person(name){
    // 属性
    this.name = name;
    
    // 方法
    if(typeof this.sayName != "function") {
        Person.prototype.sayName = function(){};
    }
}
```

6 寄生构造函数模式

特点：创建一个包装函数封装创建对象的代码，然后再返回新创建的对象。**类似工厂模式，不同的是使用new实例包装函数**

适用场景：在特殊情况下为对象创建构造函数

缺点：返回的对象与构造函数的原型属性之间没有关系，无法用instanceof确定对象类型，故可以使用其他模式的情况下不推荐此模式

```
function Person(name){
    var o = new Object();
    o.name = name;
    
    o.sayName = function(){
        alert(this.name);
    }
    return o;
}

var friend = new Person('Tom');
```

7 稳妥构造函数模式

特点：没有公共属性，**类似寄生模式，不同的是新创建的实例方法不引用this的对象；不使用new调用构造函数**

适用场景：安全环境或者防止数据被其他程序改动时用

缺点：无法用instanceof确定对象类型

```
function Person(name){
    var o = new Objcet();
    
    // 可以定义私有变量和函数
    
    // 添加方法,仅本方法访问得到name
    o.sayName = function(){
        alert(name);
    };
    
    return o;
}

var friend = Person('yingji');
```

##### 继承

只支持实现继承，主要依靠**原型链**来实现

1 原型链

**实现的本质是重写原型对象**，以父类的实例代之

```
function Super(){}
function Sub(){}

// 继承
Sub.prototype = new Super();
```

1.1 默认的原型

**指向Object.prototype**,这也是自定义类型都会继承toString()、valueOf()等默认方法的原因

1.2 确定原型和实例的关系

```
// instanceof操作符
alert(instance instanceof Object);

// isPrototypeOf()
alert(Super.prototype.isPrototypeOf(instance));
```

1.3 不能使用字面量创建原型方法

因为会重写原型链

1.4 **原型链的问题**

- 包含引用类型值的原型，会被共享；
- 没有办法在不影响所有实例的情况下，给超类的构造函数传参

故实际中很少单独使用原型链

2 借用构造函数

实现的**本质是在子类构造函数的内部调用超类构造函数**

```
function Sub(){
    Super.call(this);
}
```

- 优点：可以向超类构造函数传参
- 缺点：函数无法复用，超类定义的方法对子类不可见

故实际中也很少单独使用借用构造函数技术

3 **组合继承**

思路：
- 使用原型链实现对原型属性和方法的继承
- 借用构造函数来实现对实例属性的继承

缺点：会调用两次超类构造函数，只是第一次创建的属性被屏蔽而已，可用寄生组合式继承解决

```
function Super(name){
    this.name = name;
    this.colors = ["red"];
}

Super.prototype.sayName = function(){
    alert(this.name);
};

function Sub(name,age){
    // 继承属性
    Super.call(this,name);
    this.age = age;
}

// 继承方法
sub.prototype = new Super();
sub.prototype.constructor = Sub;
sub.prototype.sayAge = function(){
    alert(this.age);
};
```

4 原型式继承

思路：对给定对象进行浅复制

适用场景：只想让一个对象和另一个对象保持类似

优点：不必预先定义构造函数

缺点：引用类型的值会共享

`Object.create()` IE9+，传一个参数时同`object()`
```
var person = {
    name: "tom"
};

// 第二个属性可选，格式参照Object.defineProperties()
var anotherPerson = Object.create(person, {
    name: {
        value: "xiaoming"
    }
});
```

5 寄生式继承

思路：类似寄生构造函数和工厂模式,创建一个封装继承过程的函数，加强函数后返回对象

适用场景：在主要考虑对象而不是自定义类型和构造函数的情况

缺点：无法做到函数复用

```
function createAnother(original){
    var clone = object(original); // 创建新对象
    clone.sayHi = function(){}; // 增强函数
    
    return clone;
}

var person = {
    name: "tom"
};

var anotherPerson = createAnother(person);
```

6 **寄生组合式继承**

思路：使用寄生式继承来继承超类的原型，再将结果指定给子类的原型

优点：解决组合继承调用两次超类构造函数的问题,避免创建不必要的属性，是引用类型最理想的继承范式

```
function inheritPrototype(sub,super){
    var prototype = object(super.prototype); // 创建对象
    prototype.constructor = sub; // 增强对象
    sub.prototype = prototype; // 指定对象
}

function Super(name){
    this.name = name;
    this.color = ["red"];
}
Super.prototype.sayName = function(){}

function Sub(name,age){
    // 继承属性
    Super.call(this,name)
    
    this.age = age;
}

// 组合继承
// Sub.prototype = new Super();

// 替换前面为子类型原型赋值的语句
inheritPrototype(Sub,Super);
Sub.prototype.sayAge = function(){};
```

## 7 函数表达式

函数声明提升，函数表达式使用前则需要先赋值

##### 递归

```
function factorial(num){
    if(num <= 1) {
        return 1;
    } else {
        // return num * factorial(num-1);
        // 用arguments.callee代替函数名，严格模式下不能用
        return num * arguments.callee(num-1);
    }
}
```

##### 闭包

闭包是指**有权访问另一个函数作用域的变量的函数**，常见的闭包是在函数内部创建另一个函数

作用域本质是**一个指向变量对象的指针列表**

缺点：占用更多内存，需要谨慎使用

1 闭包与变量

**副作用：只能取得包含函数中任何变量的最后一个值**

```
function fn(){
    var result = new Array();
    
    for(var i=0; i < 10; i++) {
        result[i] = function(){
            return i;
        };
    }
    
    return result; // 10个10
}
```

因为每个函数的作用域链中豆保存着fn函数的活动对象，所以引用的都是同一个i，故会出现10个10，作如下修改

```
result[i] = function(num){
    return function(){
        return num;
    };
}(i);
```

2 关于this对象

**匿名函数的执行环节具有全局性**，因此其this通常指向window

ps：arguments也存在同样的问题

3 内存泄漏

闭包会引用包含函数的整个活动对象，在不用之后应该将包含的变量置null,以便顺利回收

##### 模仿块级作用域


##### 私有变量

## 21 Ajax与Comet

Ajax的核心是XMLHttpRequest对象(XHR)

##### XMLHttpRequest对象

1 XHR的用法

```
// 创建
var xhr = createXHR();
xhr.onreadystatechange = function(){
    if(xhr.readyState == 4) {
        // 状态码判断
        if((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
            alert(xhr.responseText);
        } else {
            alert('Request was unsuccessful:' + xhr.status);
        } 
    }
};

// 启动一个请求：请求的类型、url、是否异步发送
xhr.open('get', 'example.php', true)
// 发送：如不需要主体发送请求则传入null
xhr.send(null);

// 接收到响应前可取消异步请求
xht.abort();
```

xhr.readyState: 请求当前活动阶段
- 0: 未初始化
- 1: 刚调用open()
- 2: 刚调用send()
- 3: 接收到部分响应
- **4: 接收到全部响应**

另外，由于内存原因不建议复用XHR对象

2 HTTP头部信息

使用`setRequestHeader()`可以自定义请求头部信息，open之后send之前调用

```
xhr.setRequestHeader('MyHeader','MyValue');

// 获取
var myHeader = xhr.getResponseHeader('MyHeader');
var allHeader = xhr.getAllResponseHeaders();
```

3 GET请求

拼接参数以及使用`encodeURIComponent()`编码

```
function addURLparam(url, name, value){
    url += (url.indexOf('?') == -1 ? '?' : '&');
    url += encodeURIComponent(name) + "=" encodeURIComponent(value);
    return url;
}
```

4 POST请求

模仿表单提交,使用`serialize()`将表单数据序列化后再发送

```
xhr.open('post', 'test.php', true);
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
var form = document.getElementById('user-info');
xhr.send(serialize(form));
```

##### XMLHttpRequest 2级

1 FormData

为序列化表单以及创建与表单格式相同的数据提供了便利，不必明确设置请求头部

```
xhr.send(new FromData());
```

2 超时设定

IE8+ timeout属性，规定时间没有接受到请求则触发timeout事件，并调用ontimeout事件处理程序

```
xhr.timeout = 1000;
xhr.ontimeout = function(){
    alert('did not return in a second');
}
```

3 overrideMimeType()

重写响应的MIME类型，**在send之前调用**
```
// 强迫将响应当做XML而非纯文本来处理
xhr.overrideMimeType('text/xml');
```

##### 进度事件

- loadstart：在接收到相应数据的第一个字节时触发。
- progress：在接收相应期间持续不断触发。
- error：在请求发生错误时触发。
- abort：在因为调用abort()方法而终止链接时触发。
- load：在接收到完整的相应数据时触发。
- loadend：在通信完成或者触发error、abort或load事件后触发。

1 load事件

Firefox、Operan、Chrome和Safari

```
xhr.onload = function () {
    if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
        alert(xhr.responseText);
    } else {
        alert("Request was unsuccessful: " + xhr.status);
    }
};
```

2 progress事件

progress事件会在浏览器接收新数据期间周期性地触发。而onprogress事件处理程序会接收到一个event对象，其target属性是XHR对象，但包含着三个额外的属性：lengthComputable、loaded和total。**open之前调用**

其中，
- lengthComputable 表示进度信息是否可用的布尔值
- loaded 表示已经接收的字节数
- total 表示根据Content-Length响应头部确定的预期字节数

```
// 创建进度指示器
xhr.onprogress = function (event) {
    var divStatus = document.getElementById("status");
    if (event.lengthComputable) {
        divStatus.innerHTML = "Recived" + event.loaded + " of " + event.total + " bytes";
    }
}
```

##### 跨域与资源共享CORS

W3C标准，需要服务器设置header ：Access-Control-Allow-Origin

优点:支持所有类型的http请求;

缺点:IE10+

```
// 后端开启CORS权限, *表示允许任何域
// 请求和响应不包含cookie
Access-Control-Allow-Origin: https://blog.zhangyingji.cn
```

图像Ping

原理: img标签跨域不受限

应用场景: 常用于跟踪用户点击页面或动态广告曝光次数

优点: 兼容性好

缺点: 仅限GET；无法访问服务器的响应文本，单向通信

```
var img = new Image();
// 如此只要请求完成就能得到通知
img.onload = img.onerror = function(){
    alert("Done");
};
img.src = "http://www.example.com/test?name=zhangyingji";
```

JSONP

由*回调函数*和*数据*组成，需要服务器配合一个callback函数

原理: script标签跨域不受限

优点: 简单易用，相对于图像Ping能够直接访问响应文本，双向通信

缺点: 仅限GET；需要确保其他域的安全；难以确定JSONP请求是否失败

```
function handleResponse(response){
    alert(response);
}

var script = document.createElement("script);
script.src = "http://freegeoip.net/json/?callback=handleResponse";
document.body.insertBefore(script,document,body.firstChild);

// JQuery
$(function(){
    $.ajax({
        type: "get",
        async: false,
        url: "",
        dataType: "jsonp",
        // 传递给请求处理程序或页面的，用以获得jsonp回调函数名的参数名(一般默认为:callback)
        jsonp: "callback",
        // 回调函数名称，默认为jQuery自动生成的随机函数名，也可以写"?"，jQuery会自动处理数据 jsonpCallback:"flightHandler",
        success: function(json){
            alert('success');
        },
        error: function(){
            alert('fail');
        }
    }); 
});
```

反向代理

可使用nginx在nginx.conf中进行配置

## 23 离线应用与客户端存储
##### 离线检测
```
// 加载后取得初始状态
if(navigator.onLine) {
    // 正常
} else {
    // 执行离线状态时的任务
}

// HTML5的两个事件
// 再检测是否变化
EventUtil.addHandler(window,"online",function(){
    alert("online");
)};
EventUtil.addHandler(window,"offline",function(){
    alert("offline");
)};
```

##### 应用缓存

推荐阅读HTML5Doctor的[Go offline with application cache](http://html5doctor.com/go-offline-with-application-cache)

##### 数据存储

参考我的另一篇笔记[cookie、localStroage与sessionStroage](https://blog.zhangyingji.cn/2018/09/10/cookie-localStroage-sessionStroage/)

## 24 最佳实践
##### 可维护性

缩进4个空格

注释: 函数/方法、大段代码、复杂算法