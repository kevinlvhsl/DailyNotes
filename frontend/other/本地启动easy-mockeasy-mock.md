## easy-mock

1、先克隆下easy-mock项目
`git clone git@github.com:easy-mock/easy-mock.git`
并安装依赖  yarn

2、在easy-mock目录下新建一个data目录，用来放置数据

3、启动mongodb

/Users/liangxiaojun/Documents/mongodb/bin/mongod --dbpath ./data

4、在easy-mock项目下的config目录下 新建一个json文件，用来指向db存放
  取名叫local.json, 在其中加入以下内容
  x-monitor: 这个easy-mock服务的项目名
  ```
    {
      "db": "mongodb://localhost/x-monitor"
    }
  ```
5、 启动easy-mock项目 yarn dev

在浏览器输入
http://localhost:27017/ 查看mongodb是否启动成功

http://localhost:7300/  打开mock服务



6、导入swagger数据
找到swagger地址域名。 然后在后面添加 /v2/api-docs  => https://adair-dev.zhongan.io/v2/api-docs  填到项目的swagger地址栏上，然后同步就能获取到swagger上的所有接口了。。。。
