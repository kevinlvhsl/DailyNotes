## Weex 先占个坑
----

一套用js来写native的开源框架
[weex](https://github.com/alibaba/weex)


+ Clone 项目 `git clone https://github.com/alibaba/weex.git`
+ 命令行（windows 请用 git-bash）进入 weex 项目根目录
+ 安装依赖`npm install`，如果安装太慢或出错，可以使用 cnpm
  `rm -rf node_modules`
  `npm install -g cnpm`
  `cnpm install`
常规操作

+ 命令行（windows 请用 git-bash）进入 weex 项目根目录
+ 启动项目 ./start
+ H5 预览
   浏览器访问 http://localhost:12580/index.html?page=./examples/build/index.js
+ Android 预览
  下载 Playground 所有 Demo 源码在 /examples
  找个二维码工具，生成 http://ip:12580/examples/build/index.js， 然后用 Playground 扫码
+ iOS 预览
   支持本地打包，暂不支持 AppStore 下载
   找个二维码工具，生成 http://ip:12580/examples/build/index.js， 然后用 Playground 扫码
+  新增 demo
+  添加 demo， examples/demo123.we
+  重启 ./start


+ 在test目录下新建一个.we结尾的文件  内容大概如下：
```
<template>
  <div style="flex-direction: column;">
    <slider class="slider" interval="{{intervalValue}}" auto-play="{{isAutoPlay}}" >
      <div class="slider-pages" repeat="{{itemList}}" onclick="goWeexSite" >
        <image class="thumb" src="{{pictureUrl}}"></image>
        <text class="title">{{title}}</text>
      </div>
    </slider>

  <div class="container" onclick="goWeexSite" >
    <div class="cell">
        <image class="thumb" src="http://t.cn/RGE3AJt"></image>
        <text class="title">JavaScript</text>
    </div>
    <div class="cell">
        <image class="thumb" src="http://t.cn/RGE3uo9"></image>
        <text class="title">Java</text>
    </div>
    <div class="cell">
        <image class="thumb" src="http://t.cn/RGE31hq"></image>
        <text class="title">Objective C</text>
    </div>
  </div>
</template>

<style>
  .cell { margin-top:10 ; margin-left:10 ; flex-direction: row; }
  .thumb { width: 200; height: 200; }
  .title { text-align: center ; flex: 1; color: grey; font-size: 50; }
  .slider {
    margin: 18;
    width: 714;
    height: 230;
  }
  .slider-pages {
    flex-direction: row;
    width: 714;
    height: 200;
  }
</style>

<script>
module.exports = {
    data: {
      intervalValue:"1000",
      isShowIndicators:"true",
      isAutoPlay:"true",
      itemList: [
        {title: 'Java', pictureUrl: 'http://t.cn/RGE3uo9'},
        {title: 'Objective C', pictureUrl: 'http://t.cn/RGE31hq'},
        {title: 'JavaScript', pictureUrl: 'http://t.cn/RGE3AJt'}
      ]
    },
    methods: {
      goWeexSite: function () {
        this.$openURL('http://alibaba.github.io/weex/')
      }
    }
}
</script>
```
 + 在根目录下 执行命令
 `weex test/test-list.we --qr -h 192.168.2.103`
 + 然后在当前窗口就会弹出一个二维码。 用payground 扫描即可预览



