# 开发一些笔记



### 1、laravel框架对象和数组混合，

​         

​     laravel查询数据默认是数组对象，可是redis 哈希表保存的确实数组，在做缓存时，输出出现对象和数组问题

解决方法就是在查询数据库时查询的是数组

​    

```php
<?php
use PDO;
DB::setFetchMode(PDO::FETCH_ASSOC);  //加入这个
DB::table($tabal)->first();   //查询出来的就是数组
```

  

# linux一些笔记



### 一、linux文件夹权限问题

​        比如该文件夹oafile不给其它人看到 执行操作

​         **mzoa@meizhao-S1200BTL:~$ chown  root:root oafile**/ 

​         **mzoa@meizhao-S1200BTL:~$ chmod -R 700 oafile/**

  