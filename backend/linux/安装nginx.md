## 安装nginx
也是使用apt-get
+ `sudo apt-get install nginx`
+ 接下来需要对Nginx进行一些配置：
```
sudo apt-get install nginx
sudo rm sites-enabled/default
sudo touch /etc/nginx/sites-available/ghost
sudo nano /etc/nginx/sites-available/ghost
```
+ 然后把这些代码粘贴进去：
```
server {
    listen 80;
    server_name your_domain.tld;
###修该为你的域名
    location / {
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   Host      $http_host;
        proxy_pass         http://127.0.0.1:2368;
    }
}
```
然后建立一个链接，将你新建的配置告诉Nginx：
`sudo ln -s /etc/nginx/sites-available/ghost /etc/nginx/sites-enabled/ghost`
然后重启Nginx：
`sudo service nginx restart`


来源：知乎 链接：https://www.zhihu.com/question/22755373/answer/68730626

接下来创建一个新的用户，并给与他权限：sudo adduser --shell /bin/bash --gecos 'Ghost application' ghost
sudo chown -R ghost:ghost /var/www/ghost/
然后用ghost用户使用系统：su - ghost
现在我们要开启Ghost：cd /var/www/ghost
npm start --production
### [安装ghost](安装ghost.md)

