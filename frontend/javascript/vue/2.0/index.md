对2.0的解读学习
http://www.kancloud.cn/zmwtp/vue2/148822
> Vue\                ;根目录
    benchmarks\     ;测试目录
    build\          ;构建目录
    dist\           ;生成目录
    examples\       ;Demo目录
    src\            ;源代码目录
    test\           ;测试目录
    
> 源代码实现目录(vue\src)

Vue\src\
    compiler\       ;模板编译实现
    core\           ;Vue核心实现
    entries\        ;生成入口实现
    platforms\      ;渲染平台实现
    server\         ;服务器渲染实现
    shared\         ;基础工具目录
> 模块组织(\vue\build\alias.js)
```
    var path = require('path')
    
    module.exports = {
      vue: path.resolve(__dirname, '../src/entries/web-runtime-with-compiler'),
      compiler: path.resolve(__dirname, '../src/compiler'),
      core: path.resolve(__dirname, '../src/core'),
      shared: path.resolve(__dirname, '../src/shared'),
      web: path.resolve(__dirname, '../src/platforms/web'),
      server: path.resolve(__dirname, '../src/server')
    }
```
今天发现vue-router2.0 中用到了HTML5History 的api。 顺手将 history的api来粘贴一下
> history.pushState(data[,title][,url]);//向历史记录中追加一条记录，data是一个js对象，可以是任何格式的json数据，title参数暂时不起作用，我亲自试了也确实如此。参数url是指地址栏中的地址值，不填则保持当前url

history.replaceState(data[,title][,url]);//替换当前页在历史记录中的信息。参数与上面一致。

history.state;//是一个属性，可以得到当前页的state信息。

window.onpopstate;//是一个事件，在点击浏览器后退按钮或js调用forward()、back()、go()时触发。监听函数中可传入一个event对象，event.state即为通过pushState()或replaceState()方法传入的data参数。

>  还原ajax程序中浏览器后退按钮的功能。其实这个应用已经被大家广泛熟知了，由于ajax的固有缺点（无法使用浏览器后退按钮返回上一页），通过在发起ajax请求时在历史记录中添加一条记录并修改地址栏中的值，来模拟一个正常的跳转，同时仍然保留ajax异步加载的优点。方法如下：
```
var title = '另一篇随笔';
var url = 'http://www.cnblogs.com/lvdabao/p/另一篇随笔.html';
var state = {title:title,url:url};
history.pushState(state,title,url);//第三个参数url的值将会出现在地址栏
```
> 保存异步请求的参数，在页面返回时重现原来页面上的动态数据。具体需求是这样的：比如我们处在一个搜索结果列表页，页面上的内容是根据搜索条件动态得到的，我们可以点击其中一项进行详情预览（发ajax请求），在详情页点击“返回”时，我们希望原来的搜索数据还在，而不是变回列表页初始加载时的数据。以前，我们可以用回传参数的方式解决这样的需求，但那样做的缺点就是有大量的数据需要来回传递，如果页面层级较多，将会很不方便。那么现在，我们结合使用history的onpopstate事件，便可用完成这样的功能。举例来说：

```
<body>
<p>HTML5 history API 介绍</p>
<a href="javascript:void(0)" id="pushstate">history.pushState(data, title [, url])</a>&nbsp;&nbsp;&nbsp;&nbsp;
<a href="javascript:void(0)" id="replacestate">history.replaceState(data, title [, url]) </a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="javascript:void(0)" id="onpopstate">window.onpopstate</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<a href="javascript:void(0)" id="back">返回</a>
<div id="loaddiv"></div>
<script>

$(function(){
    
    var loaddiv = $('#loaddiv');
　　
　　//点击不同的链接，分别在loaddiv中加载不同的内容

    $('#pushstate').click(function(){
        loaddiv.load('1.php?stype=push');
        history.pushState({title:'push',url:'1.php?stype=push'});
        });
    $('#replacestate').click(function(){
        loaddiv.load('1.php?stype=replace');
        history.pushState({title:'replace',url:'1.php?stype=replace'});
        });
    $('#onpopstate').click(function(){
        loaddiv.load('1.php?stype=onpop');
        history.pushState({title:'onpop',url:'1.php?stype=onpop'});
        });

　　//点击返回，让浏览器后退一步
    $('#back').click(function(){
        history.back();
        });
       
　　//兼听popstate事件，可以取到e.state的值，其中保存了你调用pushState方法时传入的数据，根据数据中的url异步加载相应内容。便实现了点击返回时页面上的数据保持是上次加载过的。
    window.onpopstate = function(e){
        if(e.state){
            loaddiv.load(e.state.url);
            }
    }
    
    });
</script>
</body>
```

