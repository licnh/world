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
 