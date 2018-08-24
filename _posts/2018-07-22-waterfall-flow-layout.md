---
layout:     post
title:      "瀑布流布局"
subtitle:   ""
date:       2018-07-22 22:50:00
author:     "zhangyingji"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - JavaScript
    - CSS
---

## 思路

固定列数的浮动布局：
- 根据设备屏幕的宽度和加载图片的宽度来固定列数，之后又获取每一列图片的高度，将要加载的图片放在高度最小的那一列图片下面，循环数组不断的寻找高度最小的那一列图片，将图片放在下面实现基本的布局效果
- 创建一个滚动条监听事件（当最后一张图片距顶的高度 < 屏幕的高度+滚动条滚动的距离）时，就触发我们在页面动态的添加图片的事件（用JavasSript在Html DOM创建节点，并为其添加根元素）

## 步骤

1. 父元素设相对定位
2. 获取父元素、所有clsss为box的元素、盒子的宽度width
3. 计算页面显示的列数并取整（页面宽/box宽）
4. 设置main的宽
5. 用一个数组harr放第一行图片的高度，获取其中最小高度及其索引index
6. 子元素设绝对定位，则第二行的图片的top和left分别为最小者的高和width*index，并更新数组

## 原生JS实现

```
window.onload=function(){
waterfall('main','pin');
var dataInt={'data':[{'src':'1.jpg'},{'src':'2.jpg'},{'src':'3.jpg'},{'src':'4.jpg'}]}; // json
    
window.onscroll=function(){
       if(checkscrollside()){
            var oParent = document.getElementById('main');// 父级对象
            for(var i=0;i<dataInt.data.length;i++){
                var oPin=document.createElement('div'); //添加 元素节点
                oPin.className='pin';                   //添加 类名 name属性
                oParent.appendChild(oPin);              //添加 子节点
                var oBox=document.createElement('div');
                oBox.className='box';
                oPin.appendChild(oBox);
                var oImg=document.createElement('img');
                oImg.src='./images/'+dataInt.data[i].src;
                oBox.appendChild(oImg);
            }
            waterfall('main','pin');
        };
    }
}

function waterfall(parent,pin){
    var oParent=document.getElementById(parent); // 父级对象
    var aPin=getClassObj(oParent,pin); // 获取存储块框pin的数组aPin
    // var aPin = document.getElementsByClassName('pin'); // IE78以下不适用
    var iPinW=aPin[0].offsetWidth; // 一个块框pin的宽
    //每行中能容纳的pin个数【窗口宽度除以一个块框宽度】
    var num=Math.floor(document.documentElement.clientWidth/iPinW);
   //设置父级居中样式：定宽+自动水平外边距
    oParent.style.cssText='width:'+iPinW*num+'px;ma rgin:0 auto';
    var pinHArr=[];//用于存储 每列中的所有块框相加的高度。
    for(var i=0;i<aPin.length;i++){//遍历数组aPin的每个块框元素
        var pinH=aPin[i].offsetHeight;
        if(i<num){
            pinHArr[i]=pinH; //第一行中的num个块框pin 先添加进数组pinHArr
        }else{
            var minH=Math.min.apply(null,pinHArr);//数组pinHArr中的最小值minH
            var minHIndex=getminHIndex(pinHArr,minH);
            aPin[i].style.position='absolute';//设置绝对位移
            aPin[i].style.top=minH+'px';
            aPin[i].style.left=aPin[minHIndex].offsetLeft+'px';
            //数组 最小高元素的高 + 添加上的aPin[i]块框高
            pinHArr[minHIndex]+=aPin[i].offsetHeight;//更新添加了块框后的列高
        }
    }
}

   /*
    *通过父级和子元素的class类 获取该同类子元素的数组
    */
function getClassObj(parent,className){
    var obj=parent.getElementsByTagName('*');//获取 父级的所有子集
    var pinS=[];//创建一个数组 用于收集子元素
    for (var i=0;i<obj.length;i++) {//遍历子元素、判断类别、压入数组
        if (obj[i].className==className){
            pinS.push(obj[i]);
        }
    };
    return pinS;
}

   /*
    *获取 pin高度 最小值的索引index
    */
function getminHIndex(arr,minH){
    for(var i in arr){
        if(arr[i]==minH){
            return i;
        }
    }
}

function checkscrollside(){
    var oParent=document.getElementById('main');
    var aPin=getClassObj(oParent,'pin');
    // 创建【触发添加块框函数waterfall()】的高度：
最后一个块框的距离网页顶部+自身高的一半(实现未滚到底就开始加载)
    var lastPinH=aPin[aPin.length-1].offsetTop+Math.floor(aPin[aPin.length-1].offsetHeight/2);
    // 注意解决兼容性
    var scrollTop=document.documentElement.scrollTop||document.body.scrollTop;
    var documentH=document.documentElement.clientHeight;//页面高度
    return (lastPinH<scrollTop+documentH)?true:false;//到达指定高度后 返回true，触发waterfall()函数
}
```

## JQuery实现

```
$(window).on('load',function(){
    waterfall();
    var dataInt={'data':[{'src':'1.jpg'},{'src':'2.jpg'},{'src':'3.jpg'},{'src':'4.jpg'}]};
    $(window).on('scroll',function(){
        if(checkScrollSlide){
            $.each(dataInt.data,function(key,value){
            var oBox = $('<div>').addClass('box').appendTo($('#main'));
            var oPic  = $('<div>').addClass('pic').appendTo($(obox));
            var oImg = $('<img>').attr('src','images/' +$(value).attr('src')).appendTo($(oPic));
            })
            waterfall();
        }
    })
    function waterfall(){
        var $boxs = $('main>div');
        var w = $boxs.eq(0).outerWidth();
        var cols = Math.floor($(window).width()/w);
        $('main').width(w*cols).css('margin','0 auto');
        var hArr = [];
        $boxs.each(function(index,value){ // value为dom对象
        var h = $boxs.eq(index).outerWidth;
        if (index < cols) {
            hArr[index] = h;
        }else {
            var minH = Math.min.apply(null,hArr);
            var minHIndex = $.inArray(minH,hArr);
            $(value).css({
            'position':'absolute',
            'top':minH + 'px',
            'left':minHIndex*w+'px'
            })
            hArr[minHIndex] += $boxs.eq(index).outHeight();
            }
        })
    }
    
    function checkscrollside(){
        var $lastBox = $('main>div').last();
        var lastBoxDis = $lastBox.offset().top + Math.floor($lastBox.outerHeight()/2);
        var scrollTop = $(window).scrollTop();
        var documentH = $(window).height();
        return (lastBoxDis < scrollTop + documentH)? true:false;
    ｝
)}
```

## CSS3实现

性能高，列宽会随浏览器变换导致用户体验不好，图片顺序为垂直排列

```
.container{
    -webkit-column-width:160px; // 列宽
    -moz-column-width:160px; 
    -webkit-column-gap:5px; // 列间距
    -moz-column-gap:5px;
}

/* 数据块 */
.container div{
    width:160px;
    margin:4px 0;
}
```



