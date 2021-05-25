### windows下从零开始安装laravel-admin

注释：官方文档说php>=7.0 ，最好php版本是7.1的，我用其他版本7.2 7.3都出现各种问题。

 参考文档：https://laravel-admin.org/docs/zh/installation



1、设置composer为国内镜像，国内的防火墙太给力了；

   `composer config -g repo.packagist composer https://packagist.phpcomposer.com`

 2、 安装laravel 我没有指定版本直接是默认安装

   `composer global require "laravel/installer"`

  3、生成项目文件 

  `composer create-project --prefer-dist laravel/laravel laravel-admin`

 4、修改.env文件数据库的配置文件；

​     自己先在数据库中创建一个数据库，以访错误，随便把 /confi/database.php 的数据库配置也配置了；

5、cd 进入到laravel-admin下执行命令

​    `composer require encore/laravel-admin`

​    这个过程估计是我的网络问题有点久，要是有失败的重新执行；

6、然后运行下面的命令来发布资源

 `php artisan vendor:publish --provider="Encore\Admin\AdminServiceProvider"`

  在该命令会生成配置文件config/admin.php，可以在里面修改安装的地址、数据库连接、以及表名，建议都是用默认配置不修改。



7、然后运行下面的命令完成安装

 `php artisan admin:install`

 如果出现：SQLSTATE[42000]

请查看：https://github.com/z-song/laravel-admin/issues/1541 修改一下代码就ok



安装到这里就算ok了

配置域名访问就可以了



注释：

 因为MySQL默认的是MyISAM数据引擎，不支持事务也不支持外键，所以需要用到Innodb引擎，于是决定将 mysql的默认引擎设置为innodb。 
只要在配置文件my.cnf中的 [ mysqld] 下面加入：
default-storage-engine=INNODB
重启mysql即可