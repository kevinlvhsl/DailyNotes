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
