---
title: js数组去重
author: Mrxh
top: true
cover: true
toc: true
mathjax: false
date: 2021-07-06 21:38:38
img:
coverImg: /medias/banner/9.jpg
password:
summary: 
  我觉得需要结合实际项目需求开发，根据需求来选择哪种去重方法，根据需求来修改某些条件，或者增加条件，适合需求的才是最好的去重方法。
tags:
  - javascript
  - ES6
categories:
  - 前端
---



# 方法一

优点：简单，性能好 缺点1：在IE6-8下数组的indexOf方法不存在 缺点2：相同的字符串类型数值和数字类型的数值不会去重

```bash
function unique(arr) {
    var ret = [];

    for (var i = 0; i < arr.length; i++) {
        var item = arr[i];
        if (ret.indexOf(item) === -1) {
            ret.push(item);
        }
    }

    return ret;
}
```

# 方法二

优化方法一：在IE6-8下数组的indexOf方法不存在时，手动添加indexOf实现方法 缺点2：相同的字符串类型数值和数字类型的数值不会去重

```bash
var indexOf = [].indexOf ?
    function (arr, item) {
        return arr.indexOf(item)
    } :
    function indexOf(arr, item) {
        for (var i = 0; i < arr.length; i++) {
            if (arr[i] === item) {
                return i
            }
        }

        return -1
    }

function unique(arr) {
    var ret = []

    for (var i = 0; i < arr.length; i++) {
        var item = arr[i]
        if (indexOf(ret, item) === -1) {
            ret.push(item)
        }
    }

    return ret
}
```

# 方法三

优化方法二：写2个函数方法表示很繁琐，可以使用使用对象属性来判断 缺点：相同的字符串类型数值和数字类型的数值不会去重

```bash
function unique(arr) {
    var ret = [];
    var hash = {};

    for (var i = 0; i < arr.length; i++) {
        var item = arr[i];
        var key = typeof (item) + item;
        if (hash[key] !== 1) {
            ret.push(item);
            hash[key] = 1;
        }
    }

    return ret;
}
```

# 方法四

优化：简单，简洁快捷 缺点1：兼容低版本浏览器差 缺点2：相同的字符串类型数值和数字类型的数值不会去重

```bash
function unique(arr) {
    return [...new Set(arr)];
}
```

# 方法五

优点：兼容性好 优化点：相同的字符串类型数值和数字类型的数值会去重

```bash
function unique(arr) {
    let ret = [];
    let obj = {};
    for (var i = 0; i < arr.length; i++) {
        let item = arr[i];
        if (!obj[item]) {
            ret.push(item);
            obj[item] = 1;
        }
    }

    return ret;
}
```

思考
JS去重的方法有非常多种，以上的5种仅是代表不同的差异。我觉得需要结合实际项目需求开发，根据需求来选择哪种去重方法，根据需求来修改某些条件，或者增加条件，适合需求的才是最好的去重方法。

最简单的，我不用适配低版本浏览器，也不考虑严格的数据类型值，直接用 …new Set(arr) 最快啦~
