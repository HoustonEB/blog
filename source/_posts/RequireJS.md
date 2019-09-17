---
title: RequireJS
date: 2019-09-16 15:41:22
categories: 模块化
tags: 
- module
- RequireJS
---
### 载入脚本文件
RequireJS采用一种不同的方法去加载脚本文件和用传统的用`<script>`tags.它也可以运行的快速和被优化过,RequireJS首要的目的是模块化代码.鼓励用{% label info@moduleIDs %}来代替script标签的URLs.
RequireJS加载所有代码根据一个基础的路径(baseUrl).一个页面的入口js文件用`data-main 属性`来定义.
### data-main 入口点
```html
<!--when require.js loads it will inject another script tag
    (with async attribute) for scripts/main.js-->
<script data-main="scripts/main" src="scripts/require.js"></script>
```
<!-- more -->
注意: script标签载入脚本文件时,是异步的.所以当引入两个脚本文件时,会出现后一个脚本执行结束时间要短于第一个文件.
```html
<script data-main="scripts/main" src="scripts/require.js"></script>
<script src="scripts/other.js"></script>
```
```js
// contents of main.js:
require.config({
    paths: {
        foo: 'libs/foo-1.1.3'
    }
});
// contents of other.js:

// This code might be called before the require.config() in main.js
// has executed. When that happens, require.js will attempt to
// load 'scripts/foo.js' instead of 'scripts/libs/foo-1.1.3.js'
require(['foo'], function(foo) {

});
```
因此最好不用`data-main`属性, 而是使用一下形式.其它的脚本文件用require()调用.
```html
<script src="scripts/require.js"></script>
<script>
require(['scripts/config'], function() {
    // Configuration loaded now, safe to do other require calls
    // that depend on that config.
    require(['foo'], function(foo) {

    });
});
</script>
```
### 定义一个模块
1. 如果模块没有依赖项,只是简单的键值对,只需要传入对象.
```js
//Inside file my/shirt.js:
define({
    color: "black",
    size: "unisize"
});
```
2. 如果模块没有依赖项,只是需要在导出内容前做一些工作,可以传入function
```js
//my/shirt.js now does setup work
//before returning its module definition.
define(function () {
    //Do setup work here

    return {
        color: "black",
        size: "unisize"
    }
});
```
3. 如果有依赖项.
```js
//my/shirt.js now has some dependencies, a cart and inventory
//module in the same directory as shirt.js
define(["./cart", "./inventory"], function(cart, inventory) {
        //return an object to define the "my/shirt" module.
        return {
            color: "blue",
            size: "large",
            addToCart: function() {
                inventory.decrement(this);
                cart.add(this);
            }
        }
    }
);
```
### 配置项
```html
<script src="scripts/require.js"></script>
<script>
  require.config({
    baseUrl: "/another/path",
    paths: {
        "some": "some/v1.0"
    },
    waitSeconds: 15
  });
  require( ["some/module", "my/module", "a.js", "b.js"],
    function(someModule,    myModule) {
        //This function will be called when all the dependencies
        //listed above are loaded. Note that this function could
        //be called before the page is loaded.
        //This callback is optional.
    }
  );
</script>
```
{% note warning %}
坑1. 自定义模块引入第三方库,未生效的问题
{% endnote %}
```js
引入第三方模块时,用了别名`eg: lib/jquery`
 // THIS WILL NOT WORK
    define(['lib/jquery'], function ($) {...});

// 解决办法
requirejs.config({
    baseUrl: 'js/lib',
    paths: {
        // the left side is the module ID,
        // the right side is the path to
        // the jQuery file, relative to baseUrl.
        // Also, the path should NOT include
        // the '.js' file extension. This example
        // is using jQuery 1.9.0 located at
        // js/lib/jquery-1.9.0.js, relative to
        // the HTML page.
        jquery: 'jquery-1.9.0'
    }
});
define(['jquery'], function ($) {...});
```
参考链接: 
 - [RequireJS](https://requirejs.org/docs/api.html)
