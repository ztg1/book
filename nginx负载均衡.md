#                     nginx负载均衡



## 1、准备三台linux虚拟主机

  准备工作三台机子分别装好nginx服务器

 

  负载均衡主机A：192.168.204.129

  web主机1： 192.168.204.132

   web主机2：192.168.204.131

 

为了测试显著  修改搁置的默认index.html 文件内容分别为：A主机为`负载均衡主机` ，web1主机为`主机1 web 1` ， web2主机为`主机2 这是主机web 2`

查看效果：

 ![image-20200618104419424](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200618104419424.png)

![image-20200618104508307](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200618104508307.png)

![image-20200618104522956](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200618104522956.png)





## 2、配置主机A：

   其实这里的配置只要配置主机A就可以

​    ![image-20200618104811638](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200618104811638.png)

![image-20200618104851761](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200618104851761.png)

```
#设定负载均衡的服务器列表
upstream taishan {
    #weigth参数表示权值，权值越高被分配到的几率越大
    #下面表示131有3分之2几率，132有3分之1几率
    server 192.168.204.131 weight=2;
    server 192.168.204.132 weight=1;
}


 location / {
         proxy_pass http://taishan;#请求转向taishan定义的服务器列表
         proxy_set_header Host $host;#将请求头转发给后端服务器
         proxy_set_header X-Forward-For $remote_addr;#后端的Web服务器可以通过X-Forwarded-For获取用户真实IP
        }


```







## 3、结果显示



![image-20200618105045853](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200618105045853.png)

![image-20200618105055229](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200618105055229.png)