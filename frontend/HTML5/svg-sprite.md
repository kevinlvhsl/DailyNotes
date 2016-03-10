### svg制作sprite雪碧图

浅谈SVG Sprite
携程设计委员会 
本文引用地址：[http://ued.ctrip.com/blog/a-brief-talk-on-svg-sprite.html](http://ued.ctrip.com/blog/a-brief-talk-on-svg-sprite.html)

随着前端技术的发展，有越来越多的方法实现icon的制作，同时为了满足市面上各种大屏幕分辨率，字体图标icon font应运而生，字体图标的制作也是一种全新的设计方式，但是icon font 在windows系统下，字体较小时，锯齿问题比较严重，那么今天要讲的svg sprite，不仅可以随意改变图标大小不会产生锯齿，还能随心所欲的填充颜色。

下面来来介绍一下矢量图形SVG Sprite在页面中的应用。

#### 第一步：制作SVG图标

首先的准备一套SVG图标，我们直接到icomoon.io上下载。

1.进入网址[https://icomoon.io/app/#/select](https://icomoon.io/app/#/select)选中图标想要的图标
2.点击屏幕左下方Generate(*generate svg && more*)，不是右边的Generate fonts
3.点击左下角下载(svg,png && Download)
然后我们可以在解压文件中，找到对应的svg图标文件夹。

#### 第二步：合并SVG图标
下载好以后，目录结构中有一个 SVG 的文件夹，请再新建一个tmp的目录
在同层下新建一个gruntfile.js
我们需要通过grunt的任务把多个svg图标整合到一个svg文件中。
这里需要用到自动化合并工具（grunt），grunt有个名为svgstore的插件。
关于grunt环境的安装，就不在这阐述 。

环境安装好后，在项目目录下执行下面的命令，安装插件：

`npm install grunt-svgstore --save-dev`

安装好后，可以看到grunt-svgstore文件夹里有个gruntfile.js配置文件。
我们加入以下代码：

```
module.exports = function(grunt){
    
    //初始化设置
    grunt.initConfig({
        svgstore: {
            options: {
                includedemo: true
            },
            dest:{
                files: {
                    'tmp/spretes.svg': ['SVG/*.svg']
                }
            }
        }
    })

    //建立任务监听

    grunt.loadNpmTasks('grunt-svgstore')

    grunt.registerTask('default', ['svgstore'])
}
```

svgstore: {
            options: {
                includedemo: true
            },
            dest:{
                files: {
                    'tmp/spretes.svg': ['SVG/*.svg']
                }
            }
        }

了解更多配置项：[https://www.npmjs.com/package/grunt-svgstore](https://www.npmjs.com/package/grunt-svgstore)





到这为止，一切准备就绪，只需进入到 SVG同层目录，执行命令：
```
grunt
```


运行命令后，可以看到tmp下成功创建了sprites.svg 和一个 spretes-demo.html的文件



第三步：应用

我们来看下生成文件的源代码：
```<svg xmlns="http://www.w3.org/2000/svg"><symbol viewBox="0 0 16 16" id="alarm"><title>alarm</title> 
<path d="M8 2c-3.866 0-7 3.134-7 7s3.134 7 7 7 7-3.134 7-7-3.134-7-7-7zM8 14.625c-3.107 0-5.625-2.518-5.625-5.625s2.518-5.625
5.625-5.625c3.107 0 5.625 2.518 5.625 5.625s-2.518 5.625-5.625 5.625zM14.606 4.487c0.251-0.438 0.394-0.946 0.394-1.487 
0-1.657-1.343-3-3-3-0.966 0-1.825 0.457-2.374 1.166 2.061 0.426 3.831 1.644 4.98 3.322v0zM6.374 1.166c-0.549-0.709-1.408-1.166-2.374-1.166-1.657 0-3 1.343-3 3 0 0.541 0.143 1.049 0.394 1.487 1.148-1.678 2.919-2.896 4.98-3.322z"/>
<path d="M8 9v-4h-1v5h4v-1z"/> </symbol><symbol viewBox="0 0 16 16" id="angry"><title>angry</title> 
<path d="M8 16c4.418 0 8-3.582 8-8s-3.582-8-8-8-8 3.582-8 8 3.582 8 8 8zM8 1.5c3.59 0 6.5 2.91 6.5 6.5s-2.91 6.5-6.5 6.5-6.5-2.91-6.5-6.5 2.91-6.5 6.5-6.5zM11.002 12.199c-0.612-1.018-1.727-1.699-3.002-1.699s-2.389 0.681-3.002 
1.699l-1.286-0.772c0.874-1.454 2.467-2.427 4.288-2.427s3.414 0.973 4.288 2.427l-1.286 0.772zM11.985 4.379c0.067 0.268-0.096 0.539-0.364 0.606-0.275 0.070-0.602 0.189-0.89 0.334 0.166 0.179 0.268 0.418 0.268 0.681 0 0.552-0.448 1-1 1s-1-0.448-1-1c0-0.018 0.001-0.036
0.002-0.054 0.032-0.741 0.706-1.234 1.275-1.518 0.543-0.271 1.080-0.407 1.102-0.413 0.268-0.067 0.539 0.096 0.606 0.364zM4.015 4.379c0.067-0.268 0.338-0.431 0.606-0.364 0.023 0.006 0.559 0.141 1.102 0.413 0.568 0.284 1.243
0.776 1.275 1.518 0.001 0.018 0.002 0.036 0.002 0.054 0 0.552-0.448 1-1 1s-1-0.448-1-1c0-0.263 0.102-0.503 0.268-0.681-0.288-0.144-0.614-0.264-0.89-0.334-0.268-0.067-0.431-0.338-0.364-0.606z"/> </symbol>
</svg>
```

双击打开demo文件就可以看到svg-sprite图片效果了
再来看看浏览器里页面的效果~~~



到这里svg sprite 图标就已经完成了。

兼容性：
除了ie8及以下 还有安卓4.2以下的浏览器不支持，其余常见浏览器都支持svg
ie8中还可以使用hack手法：
```
//heart-broken 为该图标生成是的名称
<svg>
    <use xlink:href="#heart-broken" />
    <!-- [if LT IE 8]><span class="icon-heart-broken"><span/><! [endif]-->
  </svg>
```


对于ie8以下，我们可以添加一个标签，使用css sprite：

为避免其他浏览器加载，可以加上条件注释。



这样就完美啦~
要修改svg 的样式
```
svg {
    height: 36px;
    width: 50px;
    fill: red; //修改填充颜色
}
```


