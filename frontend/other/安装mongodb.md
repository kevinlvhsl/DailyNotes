### mongodb安装方法网上能找到很多
之前是windows装过，也很简单，现在用mac了，手痒就安装一次。
1、下载：[下载地址](https://www.mongodb.com/download-center?jmp=nav#community)
 下载完之后，直接解压到本地就可以用的。（最好放到一个比较短路劲的目录中，找起来方便）
2、 配置data目录，
  直接将下好的文件重命名成mongodb，然后在下面新建一个data目录，表示以后的数据都放到data中
3、 启动
  进入到mongodb/bin目录，运行下面的代码启动服务
  ./mongod --dbpath ./data
  
4、检查是否启动成功
  http://localhost:27017/
--  It looks like you are trying to access MongoDB over HTTP on the native driver port.   表示成功


mongod 设置环境变量
http://www.jianshu.com/p/2d0a1ecd0c82
