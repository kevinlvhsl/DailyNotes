## 购买服务器
为了省钱，我选了[搬瓦工](https://bandwagonhost.com) 
> 选了最便宜的19.9美元一年。 用了一个优惠码，便宜了一点点
这时候需要连接远程服务器xshell 和 xftp 工具。

## 购买域名
为了不需要备案，选了国外的服务商[godaddy](https://sg.godaddy.com/zh?ci=)

然后就开始搭建翻墙工具[shadowsocks](https://www.shadowsocks.com.hk/)

+ 第一步：安装nodejs (node-v0.10.28-linux-x64)
+ 第二步：安装shadowsocks 先装pip 用pip来装   `apt-get install pip`, `pip install shadowsocks`
+ 第三步：最后装完后配置 /etc/shadowsocks.json
```
    "server":"104.194.66.153",  // 你的主机ip
    "server_port":8388,
    "local_port":1080,
    "password":"xxxxx",       // 主机用户密码
    "timeout":600,
    "method":"aes-256-cfb"
```
+ 第四步 `nohup ssserver -c /etc/shadowsocks.json -d start &`  启动命令


如果要使用kcptun加速的话，再另行安装

+ 接下来就是安装kcptun了， 这个稍微麻烦一点(这个是服务端)

1、 ```wget https://raw.githubusercontent.com/kuoruan/kcptun_installer/master/kcptun.sh```
2、 `chmod +x ./kcptun.sh`
3、 `./kcptun.sh`

>  这三行命令的意思是从网上下载kcptun.sh脚本,给这个脚本设置可执行权限,然后执行这个脚本.
执行这个脚本后会自动安装kcptun服务端及相关软件.然后进行配置.


安装客户端kcptun。 我用的mac电脑，[达尔文386下载地址](https://github.com/xtaci/kcptun/releases/download/v20170315/kcptun-darwin-386-20170315.tar.gz)

下载成功以后，解压到指定的目录， 我这里是放在根目录下，方便找到。 然后在解压目录下执行以下命令
``` sudo ./client_darwin_386 -l 127.0.0.1:8388 -r 172.93.xx.xx:29900 -mode fast -key "it's a secrect" ```
> 参数说明
8388  端口是服务器上shadowsocks启动的端口  
172.93.xx.xx  是服务器地址  
29900  是服务器kcptun默认的监听端口（建议不要改）后面的
mode fast 是默认的加速方式，与服务骑上kcptun指定的相同
-key  是kcptun 的密码 默认是这个"it's a secrect"
客户端的连接

浏览器,如果不是Mac则需要使用插件配置代理.代理设置为sock5,地址为127.0.0.1,端口为shadowsocks的local_port,默认是1080
shadowsocks,需要根据服务端设置密码及加密方式,地址为127.0.0.1,端口为kcptun的listener_port
kcptun,地址为服务器地址,端口为服务器kcptun的listener_port

如果以上安装都没有问题的话，那在本地电脑上shadowsocks 服务器配置的地方，就可以这样配置了：
原来使用服务器地址的地方，改成127.0.0.1页可以使用了
