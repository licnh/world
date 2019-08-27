##安装
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
   >在浏览器中访问 <http://localhost/admin/>
  
---
##遇到的问题

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

##其他

1. 将界面修改为中文
   > \config\app.php中修改
  `'locale' => 'zh-CN',`