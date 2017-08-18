### 命令行登录linux服务器
> 每次通过 FileZailla登录linux查看文件比较麻烦，这里记录一下本次瞎折腾的脚印

1. 首先生成本地的sshkey： 命令`ssh-keygen -t rsa`。 生成完以后， 会在用户根目录下生成一个.ssh的文件夹， 里面有公钥(id_rsa.pub)和私钥(id_rsa)。
2. 把公钥通过fileZailla 传到服务器上。 具体：把id_rsa.pub里面的内容拷贝出来，放入新建的 authorized_keys（名字不能错哦） 文件中，然后上传到服务器的根目录下/root/.ssh/下
3. 然后就能愉快的使用命令行登录了    比如 windows下使用git-bash、mac下就用命令行或iterm： ssh 用户名@主机ip -p 端口号
4. FileZailla中也要愉快的使用秘钥登录的话，在站点管理器（左上角）中，登录类型选择 秘钥登录，输入用户名，配置好端口，然后选择秘钥时定位到.ssh下的id_rsa私钥文件就可以了

#### 扩展
命令行登录还可以更简单一点，就是在本地的.ssh目录下放一个配置文件 config  （注意没有后缀）
内容的话
```
identityFile ~/.ssh/id_rsa
# 这里是别名
Host liangxiaojun 
    HostName 172.xx.xx.xx # 这里是主机ip
    port 26050
    User root
    IdentityFile ~/.ssh/id_rsa

```
+ 作用就是把私钥做一个默认指向，并且配置参数
登录的时候， 只需要 `ssh liangxiaojun` 就可以快捷登录了。 怎么样，是不是很方便O(∩_∩)O哈哈~
