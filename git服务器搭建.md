# cento7搭建git服务器

参考文档：https://www.pianshen.com/article/15211209365/

下面搭建的git服务器的简易网络拓扑图如下所示：



 ![image-20200508165848084](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508165848084.png)



## 1、**安装及配置所需软件** 

【root 用户】

[root@ebs-33384 ~] # yum install git-core openssh-server openssh-client



## 2、初始化git用户信息

​    （内容随便填写，若省略这步操作，后面的git命令无法完成）

 

[root@ebs-33384 ~] #git config --global user.name "coffee"  	

[root@ebs-33384 ~] #git config --global user.email "coffee@gmail.com"

[root@ebs-33384 ~] #git config -l

![image-20200508152459392](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508152459392.png)



## 3、下载Gitosis。

​     Gitosis是什么？在这不细说，您只需要知道它是Git权限管理系统即可。

   [root@ebs-33384 ~] #git clone https://github.com/res0nat0r/gitosis.git



​     安装python的setuptools 

​            centos7 默认是安装ptyhon的但我还是运行了一下

  [root@ebs-33384 ~] # yum  install python-setuptools



##  4、安装Gitosis。  

[root@ebs-33384 ~] #cd gitosis/
[root@ebs-33384 ~] # python setup.py install



## 5、**在Git服务器上创建git仓库用户**

​    [Git服务器，coffee@workpc1]

  1. 什么叫git仓库用户？我是这样定义的：一个“用来将管理仓库（gitosis-admin.git）以及所有的git项目仓库存储于它的home空间”的用户。git仓库用户并不一定就是git管理员！！这点必须明白。

2. 此处再罗嗦几句。这一步要创建的用户，网上绝大部分文档都取名为“git”。这点我一直没弄明白，为什么非得叫“git”，而不能是“张三”、“李四”，是Git的明文规定吗？非也！为了更好的理解本篇文章以及git服务器的工作原理，我创建的这个具有git属性的用户名字叫做“john”。（我相信这对初学者来说，对理清思路是有帮助的。当然，对于深入理解git的人来说叫啥都是一样的）
    [root@ebs-33384 ~]#useradd -m john
    [root@ebs-33384 ~]#passwd john

  

将john设置为root用户，centos创建的用户默认都不属于root用户组。 

   （这里你也可以不把john 设置为root用户在，我没有试过）

[root@ebs-33384 ~]#vi /etc/group

  ![image-20200508154012748](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508154012748.png)



注意，您不要着急敲下面的命令，只看就行，因为这些命令与《搭建git服务器》其实半毛钱关系也没有！我讲这些的目的是为了不让您再被网上的那些资料所困扰（我没有敲下面的命令）
/////////////////////////////////////////////////////

~$ sudo mkdir /home/gitrepository  
~$ sudo chown john:john /home/gitrepository/  
~$ sudo chmod 700 /home/gitrepository/
~$ sudo ln -s /home/gitrepository /home/john/repositories



我在最开始搭建git服务器的时候，也是参考网上的一些资料，按照他们说的步骤一步一步操作。当碰到上面这些操作的时候，我就蒙圈了！我不明白为什么要这么做？既然Gitosis默认状态下会将git仓库放在服务器上git用户主目录（home）下的repositories目录下，那就让它放在那呗，为什么非得搞一个链接，将repositories指向别的目录呢？难道这也是Gitosis明文规定的吗？非也！可惜，网上这些作者根本就不解释为什么这么做。虽然心中一直“不爽”，但是作为小白的我只能按着“圣典”操作。直到现在，终于理解了，上述命令只是那些作者的一些“个人爱好”而已，完全是没必要的！那些作者们您非要改变它的存放位置，那也请给出适当的解释嘛（比如说是为了防止git用户的存储空间不够用了啊什么的）。废话少说，接着讲正题.



## 6、**生成git管理员的公钥**

**[开发机window10，admin@DESKTOP-A7MHPJQ]**

  首先你window 要安装git ，打开git

   正式任命admin@DESKTOP-A7MHPJQ为git管理员

   $ ssh-keygen -t rsa #不需要密码,一路回车就行(在本地操作)

​    				![image-20200508154504895](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508154504895.png)



$ scp ~/.ssh/id_rsa.pub root@服务器的IP地址:/tmp/ #上传ssh public key到Git服务器

注意：要是你服务器ssh默认不是22端口 

​       $ scp -P 端口号  ~/.ssh/id_rsa.pub root@服务器的IP地址:/tmp/ #上传ssh public key到Git服务器

  输入root 用户密码 就可以了，这个时候公钥已经上传到cento服务/tmp/ 目录里面了



执行：

$ scp -P 22000 ~/.ssh/id_rsa.pub root@211.149.220.32:/tmp/

输入服务器密码就可以

## 7、**初始化Gitosis**

**[Git服务器，john@workpc1]**

 目前为止，Git服务器端还一直在root用户下，现切换至john用户（因为在第二步，定义了john为git仓库用户，仓库将都会存放在john的用户空间下）    



[root@ebs-33384 ~]#su john

[root@ebs-33384 ~]#cd #转至john的home目录

初始化git用户信息（内容随便填写）

[john@ebs-33384 ~]#git config --global user.name "john" 

[john@ebs-33384 ~]#git config --global user.email "john@gmail.com"





## 8、用git管理员的公钥来对Gitosis进行初始化

  上面一步我们已经切换到john用户了，现在我们要把它切换回到到root用户 ；

[root@ebs-33384 ~]# sudo -H -u john gitosis-init < /tmp/id_rsa.pub #用git管理员的公钥来对Gitosis进行初始化





执行之后，/home/john目录下出现一个repositories的目录，目录下存在一个gitosis-admin.git的git库. 其实Gitosis就是通过这个git库来管理所有git库的访问权限的。gitosis-admin的库中存在一个gitosis.conf和一个keydir的目录。其中：
1. gitosis.conf文件就是权限配置的地方（其语法及用法可以去查看相关帮助），该文件位于～/repositories/gitosis-admin.git/。用vi打开gitosis.conf文件，可看到admin@DESKTOP-A7MHPJQ对giosis-admin.git仓库具有写权限，他即是管理员。

![image-20200508155635860](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508155635860.png)

2. keydir目录下存放的是所有客户端的公钥，该目录位于～/repositories/gitosis-admin.git/gitosis-export/keydir/，公钥名字必须和配置文件中的member名字对应。

这里我们还需要对其中的一个post-update文件添加可执行的权限。（其实，在我的环境下，该文件的权限已经是755了）



[root@ebs-33384 ~]# chmod 755 ～/repositories/gitosis-admin.git/hooks/post-update

![image-20200508155858389](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508155858389.png)





截止到这，Git服务器架构搭建完毕，仓库是空的（除了自带的gitosis-admin.git仓库），配置文件也是最简单的配置。

接下来，我们来创建git项目，编辑gitosis.conf配置文件为git项目指定可操作的用户和用户所拥有的权限，为用户生成公钥，最后将所有改动上传到Git服务器。



## 9、配置gitosis-admin

**[开发机1，admin@DESKTOP-A7MHPJQ]**
目前，git管理员只有一名成员：admin@DESKTOP-A7MHPJQ，只有它有权限配置gitosis-admin。
$ git clone john@workpc1:gitosis-admin.git #获取Gitosis管理项目

 我的服务器默认不是22端口： git clone ssh://john@211.x.x.x:44000/gitosis-admin.git

这个时候代码已经clone到本地了



在当前目录下将会产生一个gitosis-admin的目录，里面有配置文件gitosis.conf和一个keydir的目录，keydir目录主要存放git用户名。

![image-20200508160502757](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508160502757.png)

$ vi gitosis-admin/gitosis.conf  #编辑gitosis-admin配置文件

![image-20200508160641918](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508160641918.png)



我们指定了project1的members，包含tiger，因此我们还需要将项目成员ztg的公钥上传到Git服务器。

## 10、 **生成客户端项目成员的公钥**



**[开发机2，ztg@xiaozhang]** 

​       开发机2 是我的虚拟机，我直接把生成好的 .ssh文件下载到我们的本地开发机1 

![image-20200508161007381](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508161007381.png)



![image-20200508161307355](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508161307355.png)





![image-20200508162545374](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508162545374.png)

（这里实际就是把开发机2的公钥放到开发1  刚刚从服务器clone来的项目 keydir文件里面并且重新命名为ztg@xiaozhang  这个名字是刚刚在客户机1配置的名字）





## 客户机1把文件上传到服务器：

 $ git add .    \#记录所有操作

$ git commit -am “xxxxx” #提交到本地仓库

$git push origin master #将本地仓库提交到Git服务器

![image-20200508162845136](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508162845136.png)







## 11、**在客户端创建项目**

**[开发机2，ztg@ztg]**



我们添加了新的git项目的信息，名称为project1，成员有admin@DESKTOP-A7MHPJQ、ztg@xiaozhang。现在来创建真正的git项目，可以在开发机1（admin@DESKTOP-A7MHPJQ），也可以在开发机2（ztg@xiaozhang）来创建这个git项目，我选择在开发机2（ztg@xiaozhang）下创建：


ztg@ztg:~$mkdir ~/project1

ztg@ztg:~$mkdir ~/project1
ztg@ztg:~$cd ~/project1
ztg@ztg:~/project1$] git init
ztg@ztg:~/project1$] touch a.txt #创建一个空文件，这步省略的话，在git push时，会报错。后面有说明
[tztg@ztg:~/project1$] git add . #新增文件 留意后面有一个点
ztg@ztg:~/project1$] git commit -am “初始化项目project1″

ztg@ztg:~/mzapp$ git remote add origin ssh://dbcgit@211.xxx.220.xx:22000/project1.git  #烦烦烦

​                       本地：git remote add origin  john@192.168.2.149:rpcbox.git

//在Ubuntu中上面报错 https://www.cnblogs.com/wuxun1997/p/10551573.html

ztg@ztg:~/mzapp$ git push origin master                       #提交文件



![image-20200508163946873](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508163946873.png)



然后就到把这个项目放到git server服务器上去.





最后返回到客户机1 clone 项目看看能克隆下面不

git clone ssh://dbcgit@211.149.220.32:22000/mzapp.git

![image-20200508165417237](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508165417237.png)



这里要是没有权限下载 修改一下文件重新上次到服务器就可以

![image-20200508170314278](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20200508170314278.png)





