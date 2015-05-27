# seajs-note

标签（空格分隔）： seajs

---

一个模块一个文件
使用define定义模块
使用use异步加载模块
使用exports对外提供接口
使用use的回调函数获取加载的模块对象

---
### seajs.config
当模块的标示很长时，可以使用alias来简化
当目录较深，或者需要跨目录调用模块时，可以使用paths来简化书写
使用preload配置项，可以在普通模块加载前，提前加载并初始化好制定模块
使用base配置项可以来配置seajs的基础路径

---
### seajs.use
用来在页面中加载一个或者多个模块，可以使用回调函数

``` javascript
seajs.use(['./a', './b'], function(a, b){
    a.do();
    b.do();
});
```

*注意：*seajs与DOM ready 事件没有任何关系，如果某些操作要确保在DOM ready 后执行，需要使用jquery等类库来保证。
```
seajs.use(['jquery', './main'], function($, main) {
    $(document).ready(function(){
        main.init();
    });
});
```

---
###define
用来定义模块，统一的写法如下：
```
define(function(require, exports, module) {
    //todo
})
```
---
###require
require用来获取制定模块的接口，类似于node
如果需要动态加载，可以使用require.async
require.async用来在模块内部异步加载一个或者多个模块

---
###exports与module.exports
模块内部对外提供接口
exports是module.exports的一个引用，在factory内部给exports重新赋值时，并不会改变module.exports的值。因此给exports赋值时无效的

module是一个对象，上面存储的与当前模块相关的属性与方法。需要注意的是module.exports的赋值需要同步执行，不能放在回调函数中
一般情况下，如果当模块的接口是某个类的实例时，需要通过module.exports来实现

---
### 加载模块
seajs.use理论上只用于加载启动，不应该出现在define中的模块代码中，在模块代码中加载其他模块时，推荐使用require.async

---
### 插件
seajs-css 是使Sea.js能够加载一个css文件，和link标签一样
seajs-style 是指提供一个seajs.importStyle 方法用于加载一段css字符串


