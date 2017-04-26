### 安装博客系统ghost
创建一个工作空间 `cd /var/www/`
+ 下载Ghost并解压
`sudo wget https://ghost.org/zip/ghost-latest.zip`
`sudo unzip -d ghost ghost-latest.zip`
> (解压的时候可能会出错，是因为没有下载解压工具unzip，执行命令下载即可，然后重复解压命令。) `sudo apt-get install unzip`

+ 安装Ghost的生产模块：
  `cd ghost/`
  `sudo npm install --production`
 > 安装时可能会报缺少包， 使用node npm 根据报错信息逐个安装
 
 + 现在我们已经安装完了，但是需要设置之后，才能启动它。
 Ghost设置：
  `sudo cp config.example.js config.js`
  这句话的意思复制config.example.js 并命名为config.js，我们要对config.js这个文件进行修改：
  `sudo nano config.js`
 > (这句话是用nano打开config.js，提示没有安装nano的话，输入以下命令安装，然后重复上一条命令：) `sudo apt-get install nano`
 
 打开以后，修改以下被标注的区域：
 ```
 config = {
    // ### Production
    // When running Ghost in the wild, use the production environment
    // Configure your URL and mail settings here
    production: {
        url: 'http://my-ghost-blog.com',
    ###将' ' 内部的内容修改为你的解析后的域名，注意带上http
        mail: {
            // Your mail settings
        },
        // 这里的数据库也可以改成mysql
        database: {
            client: 'sqlite3',
            connection: {
                filename: path.join(__dirname, '/content/data/ghost.db')
            },
            debug: false
       },

        server: {
            // Host to be passed to node's `net.Server#listen()`
            host: '127.0.0.1',
            ###将‘127.0.0.1’改为‘0.0.0.0’
            // Port to be passed to node's `net.Server#listen()`, for iisnode s$
            port: '2368'
        }
    },
```
可以去看[安装mysql](安装mysql.md)

然后CTRL + X再输入Y然后敲ENTER退出

+ 现在已经配置好了Ghost，输入：sudo npm start --production
大概会显示：> ghost@0.10.8 start /var/www/ghost
> node index

Migrations: Database initialisation required for version 003
Migrations: Creating tables...
Migrations: Creating table: posts

然后现在你就可以让你的Ghost使用2368这个端口：http://你的域名.com:2368就可以看到Ghost本尊。[http://blog.liangxiaojun.cn/](http://blog.liangxiaojun.cn/)

CTRL + C可以结束掉正在开启的Ghost
接下来要让你的Ghost一直处于运行状态。[安装nginx](安装nginx.md)

快捷启动ghost 可以用 pm2 和 forever
+ 安装pm2
`npm install -g pm2`
`NODE_ENV=production pm2 start index.js --name "ghost" `
接下来就可以 `pm2 start/stop/restart ghost  `

+ 安装forever
`npm install -g forever`
配置(在ghost目录下)： `NODE_ENV=production forever start index.js`

