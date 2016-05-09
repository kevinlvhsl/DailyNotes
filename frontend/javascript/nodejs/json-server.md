## JSON-SERVER

### 安装
------

`npm install -g json-server`

### 克隆

`Git clone https://github.com/typicode/json-server `
 依据readme.md,创建db.json 
 启动服务 json-server --watch db.json
 
 ### 应用
 + 在某个目录下安装 json-server   
 `npm install json-server`
 + 然后新建db.json
 --db.json
```
{
  "posts": [
    {
      "id": 1,
      "title": "json-server",
      "author": "kevin"
    },
    {
      "id": 2,
      "title": "路由routers 来的json-server",
      "author": "routers"
    }
  ],
  "comments": [
    {
      "id": 1,
      "body": "some comment",
      "postId": 1
    }
  ],
  "profile": {
    "name": "typicode"
  }
}
```
+ 再新建server文件
--server.js
```
var jsonServer = require('json-server')
var server = jsonServer.create()
var router = jsonServer.router('db.json')
var middlewares = jsonServer.defaults()

server.use(middlewares)
server.use(router)
server.listen(3004, function () {
  console.log('JSON Server is running')
})
```
+ 最后 运行node server.js

#### json-server 也支持自己生成js文件代替json的db
// index.js
```
module.exports = function() {
  var data = { users: [] }
  // Create 1000 users
  for (var i = 0; i < 1000; i++) {
    data.users.push({ id: i, name: 'user' + i })
  }
  return data
}
```
 + 运行命令： ` json-server index.js -p 3004`
 + 打开浏览器： localhost:3004  或 localhost:3004/users/1（用id来筛选）
