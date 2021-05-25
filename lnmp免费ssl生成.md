## lnmp 添加域名生成免费的ssl





1、vhost add 初始添加域名的时候

​     ![image-20200908144749079](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200908144749079.png)



2、已知域名添加ssl

​     输入命令**lnmp ssl add**

​    最后选择2 完成生成SSL工作

​    https://lnmp.org/faq/lnmp-vhost-add-howto.html

   80端口默认指向443 

```json
          listen 80;
        #listen [::]:80;
        server_name www.dbc19.top dbc19.top;
#        rewrite ^(.*)$ https://${server_name}$1 permanent;  //加入这个默认执行到https

```





3、手动更新域名ssl

查看地址：

http://xyuxf.com/archives/1482?__cf_chl_jschl_tk__=642dcbf98c342cd674a72e635f3e77626959ef80-1599548068-0-AVpw697xVdkyB7J7k3Yh8gwMk7JySWUMBqQ3B2R4WLN8FCPGtNJH3kVtEyZWzkoGE8NF-XCxoyVyeCyyFT9Feq4PymVn6SwaASS-akyFvbkGVg3TyWtxdulYoeMo4_WLzox-FGB4IfuqROHBY5TnDs630nP-WEqe41ZpyWpA0DAaDchnwwUYk8quV3RCaNYA3PemsC3RoJP1V0YJ1muGU3-wI2fvCPNe_Sg3antKR3inuJtH623N6P9PwePdLUjrb3_1XKBFvPHX8KxhqbedxlUFDeefYs9XaRS5ABrP0Deu



![image-20200908150003649](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200908150003649.png)









