## 环境搭建

1. 使用lnmp的一键安装脚本 [github文档](https://github.com/licess/lnmp)
2. 查看php扩展，因为laravel需要以下条件：
   - PHP >= 7.1.3
   - PHP OpenSSL 扩展
   - PHP PDO 扩展
   - PHP Mbstring 扩展
   - PHP Tokenizer 扩展
   - PHP XML 扩展
   - PHP Ctype 扩展
   - PHP JSON 扩展
   - PHP BCMath 扩展

## 安装composer

1. dc

2. 换为国内源 

   > composer config -g repo.packagist composer https://packagist.phpcomposer.com

## 安装laravel

1. composer global require laravel/installer

2. 将laravel包含到path 

   > export PATH=$PATH:$HOME/.config/composer/vendor/bin
   >
   > source /etc/profile
   >
   > chmod u+x /root/.config/composer/vendor/laravel/installer/laravel

   

3. 新建laravel项目

   > cd /home/wwwroot
   >
   > laravel new nezha

4. 用lnmp命令 新建vhost域名 www.nezha.test

   > lnmp vhost add

   再将该域名指向127.0.0.1

   > vi /etc/hosts
   >
   > 写入 > 127.0.0.1 www.nezha.test

   改写fastcgi的配置

   > vi /usr/local/nginx/conf/fastcgi.conf

   在fastcgi_param PHP_ADMIN_VALUE中加入项目的根路径，形如：

   > fastcgi_param PHP_ADMIN_VALUE "open_basedir=$document_root/:/tmp/:/proc/:/home/wwwroot/nezha/"

4. 修改.env

   > vi /home/wwwroot/nezha/.env
   >
   > 将mysql的密码改为服务器的mysql密码

## 安装laravel-admin

1. 需要装好laravel
2. 配置好数据库连接，在/.env
3. 然后在项目根目录引入laravel-admin源码：
   
   > 运行：`composer require encore/laravel-admin` 
4. 发布资源
   > 运行：`php artisan vendor:publish --provider="Encore\Admin\AdminServiceProvider"
`
5. 执行安装
   
   >运行：`php artisan admin:install`
6. 访问
   
   >在浏览器中访问 <http://localhost/admin/>  账号admin密码admin

---
## 遇到的问题

1. <http://localhost/admin/> 404
   > 在nginx中配置
   ```
   location / {
    try_files $uri $uri/ /index.php?$query_string;
   }
   ```
2. Disk \[admin] not configured, please add a disk config in config/filesystems.php.
   >在/config/filesystems.php中为admin应用加入如下配置
   ```
   'admin' => [
       'driver' => 'local',
       'root' => public_path('upload'),
       'visibility' => 'public',
       'url' => env('APP_URL') . '/upload/',
   ],
   ```

---

## 其他

1. 将界面修改为中文
   > \config\app.php中修改
    `'locale' => 'zh-CN',`
   
2. 优化composer ： 

   > composer dump-autoload --optimize

   这个命令的本质是将 PSR-4/PSR-0 的规则转化为了 classmap 的规则， 因为 classmap 中包含了所有类名与类文件路径的对应关系，所以加载器不再需要到文件系统中查找文件了。可以从 classmap 中直接找到类文件的路径。
   
3. 每次改env都要运行

   > php artisan config:clear
