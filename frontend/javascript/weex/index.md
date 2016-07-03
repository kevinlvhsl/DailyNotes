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
