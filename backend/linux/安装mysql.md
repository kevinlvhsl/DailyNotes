## linux上安装mysql
我用的是乌班图， 自带apt-get 那就直接用它了。
+ `apt-get update`, `apt-get install mysql`, `apt-get install mysql-server`  
> 安装过程中 会提示你创建用户 和输入密码，默认是root，密码也可以不填。

+ 创建好了以后就启动一下， `service mysql start`
+ 并尝试登录 `mysql -uroot -p `
