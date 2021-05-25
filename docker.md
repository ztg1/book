[Eric's Blog](https://eric_bb.gitee.io/)

[主页](https://eric_bb.gitee.io/)[文章](https://eric_bb.gitee.io/post/)[标签](https://eric_bb.gitee.io/tags/)[目录](https://eric_bb.gitee.io/categories/)

# Docker

2021-05-07 

[ Docker ](https://eric_bb.gitee.io/categories/docker/)

 约 14013 字 预计阅读 28 分钟 59 次阅读

## 文章目录

[Docker](https://eric_bb.gitee.io/post/docker/#docker)[Docker概述](https://eric_bb.gitee.io/post/docker/#docker概述)[Docker为什么会出现？](https://eric_bb.gitee.io/post/docker/#docker为什么会出现)[Docker的历史](https://eric_bb.gitee.io/post/docker/#docker的历史)[Docker能够干嘛](https://eric_bb.gitee.io/post/docker/#docker能够干嘛)[Docker安装](https://eric_bb.gitee.io/post/docker/#docker安装)[Docker的基本组成](https://eric_bb.gitee.io/post/docker/#docker的基本组成)[安装Docker](https://eric_bb.gitee.io/post/docker/#安装docker)[阿里云镜像加速](https://eric_bb.gitee.io/post/docker/#阿里云镜像加速)[回顾HelloWorld流程](https://eric_bb.gitee.io/post/docker/#回顾helloworld流程)[底层原理](https://eric_bb.gitee.io/post/docker/#底层原理)[Docker的常用命令](https://eric_bb.gitee.io/post/docker/#docker的常用命令)[帮助命令](https://eric_bb.gitee.io/post/docker/#帮助命令)[镜像命令](https://eric_bb.gitee.io/post/docker/#镜像命令)[容器命令](https://eric_bb.gitee.io/post/docker/#容器命令)[常用其他命令](https://eric_bb.gitee.io/post/docker/#常用其他命令)[小结](https://eric_bb.gitee.io/post/docker/#小结)[常用命令总结](https://eric_bb.gitee.io/post/docker/#常用命令总结)[作业练习](https://eric_bb.gitee.io/post/docker/#作业练习)[可视化](https://eric_bb.gitee.io/post/docker/#可视化)[Docker镜像讲解](https://eric_bb.gitee.io/post/docker/#docker镜像讲解)[镜像是什么](https://eric_bb.gitee.io/post/docker/#镜像是什么)[Docker镜像加载原理](https://eric_bb.gitee.io/post/docker/#docker镜像加载原理)[分层理解](https://eric_bb.gitee.io/post/docker/#分层理解)[commit镜像](https://eric_bb.gitee.io/post/docker/#commit镜像)[容器数据卷](https://eric_bb.gitee.io/post/docker/#容器数据卷)[什么是容器数据卷](https://eric_bb.gitee.io/post/docker/#什么是容器数据卷)[使用数据卷](https://eric_bb.gitee.io/post/docker/#使用数据卷)[实战：安装MySQL](https://eric_bb.gitee.io/post/docker/#实战安装mysql)[具名和匿名挂载](https://eric_bb.gitee.io/post/docker/#具名和匿名挂载)[初识DockerFile](https://eric_bb.gitee.io/post/docker/#初识dockerfile)[数据卷容器](https://eric_bb.gitee.io/post/docker/#数据卷容器)[DockerFile](https://eric_bb.gitee.io/post/docker/#dockerfile)[DockerFile介绍](https://eric_bb.gitee.io/post/docker/#dockerfile介绍)[DockerFile镜像的构建](https://eric_bb.gitee.io/post/docker/#dockerfile镜像的构建)[DockerFile指令](https://eric_bb.gitee.io/post/docker/#dockerfile指令)[实战测试](https://eric_bb.gitee.io/post/docker/#实战测试)[用实战看CMD和ENTRYPOINT的区别](https://eric_bb.gitee.io/post/docker/#用实战看cmd和entrypoint的区别)[实战：Tomcat镜像](https://eric_bb.gitee.io/post/docker/#实战tomcat镜像)[发布自己的镜像](https://eric_bb.gitee.io/post/docker/#发布自己的镜像)[小结](https://eric_bb.gitee.io/post/docker/#小结-1)[Docker网络](https://eric_bb.gitee.io/post/docker/#docker网络)

# Docker

> Docker学习
>
> - Docker概述
> - Docker安装
> - Docker命令
>
> 镜像命令
>
> 容器命令
>
> 操作命令
>
> - Docker镜像
> - 容器的数据卷
> - DockerFile
> - Docker网络原理
> - IDEA整合Docker
> - Docker Compose
> - Docker Swarm
> - CI/CD Jenkins

## Docker概述

### Docker为什么会出现？

一款产品：开发–上线 两套环境 应用环境，应用配置

开发–运维 问题：我的电脑可以运行，版本更新，导致服务不可用，对于运维来说，考验比较大

开发即运维！

环境配置十分麻烦，每一个机器都要部署环境（集群Redis ES Hadoop）费事费力。

发布一个项目（jar +（Redis MySQL jdk ES）），项目能够带上环境的安装打包！

之前在服务器配置一个应用的环境 Redis MySQL jdk ES Hadoop，配置非常麻烦，不能够跨平台。

windows，最后发布到Linux！

传统：开发jar，运维来做

现在：开发打包部署上线，一套流程做完！

java – apk – 发布 （应用商店）— 张三使用apk — 安装即可用！

java — jar（环境） —- 打包项目带上环境（镜像） — （Docker仓库：商店）— 下载我们的镜像 — 直接运行即可

Docker给以上问题，提出来解决方案！

[![image-20210503202442508](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323365_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323365_0.png)

Docker思想来自于集装箱！

JRE — 多个应用（端口冲突）–原来都是交叉的

隔离：Docker的核心思想！打包装箱，每个箱子都是相互隔离的

Docker通过隔离机制，可以将服务器利用到极致

本质：所有的技术都是因为有了问题才会不断推动去解决

### Docker的历史

2010年，几个搞IT的年轻人，就在美国成立了一家公司`dotCloud`

做一些pass的云计算服务！LXC有关的容器技术

这帮人将自己的容器化技术命名为Docker！

Docker刚刚诞生的时候没有引起行业的注意，dotCloud活不下去

2013年，Docker开放源代码，越来越多的人发现Docker优点，2014年发布了第一版

Docker为什么这么火？十分的轻巧

在容器技术出现之前，我们使用的都是虚拟机技术

虚拟机：在windows中装一个Vmware，通过这个软件我们可以虚拟一台或者多台电脑，比较笨重

虚拟机也是属于虚拟化技术，Docker容器技术，也是一种虚拟化技术！

| `1 2 ` | `vm: linux centos原生镜像（一个电脑）隔离：需要开启多个虚拟机  几个G docker: 隔离，镜像（最核心的环境 4m+jdk+mysql）十分的小巧，运行镜像就可以了 几个M 秒级启动 ` |
| ------ | ------------------------------------------------------------ |
|        |                                                              |

到现在所有的开发人员必备的技术

> 聊聊Docker

Docker是基于Go开发的

官网：https://www.docker.com/

[![image-20210503204209184](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323258_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323258_0.png)

文档地址：https://docs.docker.com/文档比较详细

仓库地址：https://hub.docker.com/

### Docker能够干嘛

> 之前的虚拟机

[![image-20210503204822802](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323678_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323678_0.png)

虚拟机技术缺点：

1、资源占用很慢

2、冗余步骤非常慢

3、启动很慢

> 容器化技术

**容器化技术不是一个完整的操作系统**

[![image-20210504143524686](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323407_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323407_0.png)

比较Docker和虚拟机技术的不同：

- 传统的虚拟机，虚拟出一套硬件，运行一个完整的操作系统，然后在这个系统上安装和运行软件
- 容器内的应用直接运行在宿主机的内容，容器没有自己的内核，也没有虚拟我们的硬件，所以就轻便了
- 每个容器内相互隔离，每个容器内都有一个属于自己的文件系统，互不影响

> DevOps（开发、运维）

**应用快速的交付和部署**

传统：一堆帮助文档，安装程序

Docker：打包镜像发布测试，一键运行

**更便捷的升级和缩扩容**

使用Docker之后，部署应用就像搭积木一样

项目打包为一个镜像，扩展服务器A 服务器B

**更简单的系统运维**

在容器化之后，我们的开发，测试环境都是高度一致的

**更高效的计算资源应用：**

Docker是内核级的虚拟化，可以在一个物理机上运行很多个容器，服务器的性能可以被运用到极致

## Docker安装

### Docker的基本组成

[![image-20210507225901074](https://gitee.com/eric_bb/image/raw/master/202105/20210507_225901693_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_225901693_0.png)

**镜像（image）：**

Docker镜像就好像是一个模板，可以通过这个模板来创建容器服务，tomcat镜像 = =>run= =>tomcat01容器（提供服务），通过这个镜像可以创建多个容器（服务或者项目就是运行在容器内）

**容器（container）：**

Docker利用容器技术，独立运行一个或者一组应用，通过镜像来创建的

启动，停止，删除，基本命令

目前就可以把这个容器理解为简单的linux系统

**仓库（repository）：**

仓库就是存放镜像的地方，分为私有仓库或者共有仓库Docker Hub，阿里云都有仓库（配置镜像加速）

### 安装Docker

> 环境准备

1、需要会一点点的linux基础

2、centos7

> 搭建虚拟机linux的注意事项：
>
> 在进行nat的静态ip地址配置时，ip子网的设置不要设置成主机一样的
>
> 比如主机地址为`222.20.60.84`，那么子网的地址设置为`222.20.40.0`改变一下地址，否则会出现主机和虚拟机不能相互ping通的情况

3、我们使用xshell连接远程服务器进行操作

> 环境查看

| `1 2 3 ` | `#系统内核是3.10以上 [root@localhost ~]# uname -r 3.10.0-1160.el7.x86_64 ` |
| -------- | ------------------------------------------------------------ |
|          |                                                              |

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 ` | `#系统版本 [root@localhost ~]# cat /etc/os-release  NAME="CentOS Linux" VERSION="7 (Core)" ID="centos" ID_LIKE="rhel fedora" VERSION_ID="7" PRETTY_NAME="CentOS Linux 7 (Core)" ANSI_COLOR="0;31" CPE_NAME="cpe:/o:centos:centos:7" HOME_URL="https://www.centos.org/" BUG_REPORT_URL="https://bugs.centos.org/" CENTOS_MANTISBT_PROJECT="CentOS-7" CENTOS_MANTISBT_PROJECT_VERSION="7" REDHAT_SUPPORT_PRODUCT="centos" REDHAT_SUPPORT_PRODUCT_VERSION="7" ` |
| ------------------------------------------------ | ------------------------------------------------------------ |
|                                                  |                                                              |

> 安装

帮助文档：

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 ` | `#1、卸载旧的版本 yum remove docker \                  docker-client \                  docker-client-latest \                  docker-common \                  docker-latest \                  docker-latest-logrotate \                  docker-logrotate \                  docker-engine #2、需要的安装包 yum install -y yum-utils #3、设置镜像的仓库 yum-config-manager \    --add-repo \    https://download.docker.com/linux/centos/docker-ce.repo #默认是国外的 yum-config-manager \    --add-repo \    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo #阿里云镜像    # 更新yum软件包索引 yum makecache fast #4、安装Docker相关的 docker-ce社区 ee企业版 yum install docker-ce docker-ce-cli containerd.io #5、启动docker systemctl start docker #6、使用docker version查看是否启动成功 [root@localhost ~]# docker version Client: Docker Engine - Community Version:           20.10.6 API version:       1.41 Go version:        go1.13.15 Git commit:        370c289 Built:             Fri Apr  9 22:45:33 2021 OS/Arch:           linux/amd64 Context:           default Experimental:      true Server: Docker Engine - Community Engine:  Version:          20.10.6  API version:      1.41 (minimum version 1.12)  Go version:       go1.13.15  Git commit:       8728dd2  Built:            Fri Apr  9 22:43:57 2021  OS/Arch:          linux/amd64  Experimental:     false containerd:  Version:          1.4.4  GitCommit:        05f951a3781f4f2c1911b05e61c160e9c30eaa8e runc:  Version:          1.0.0-rc93  GitCommit:        12644e614e25b05da6fd08a38ffa0cfe1903fdec docker-init:  Version:          0.19.0  GitCommit:        de40ad0 ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

| `1 2 ` | `#7、hello-world docker run hello-world ` |
| ------ | ----------------------------------------- |
|        |                                           |

[![image-20210504214134145](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323292_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323292_0.png)

| `1 2 3 4 ` | `#8、查看一下下载的这个hello-world镜像 [root@localhost ~]# docker images REPOSITORY    TAG       IMAGE ID       CREATED       SIZE hello-world   latest    d1165f221234   8 weeks ago   13.3kB ` |
| ---------- | ------------------------------------------------------------ |
|            |                                                              |

了解：卸载docker

| `1 2 3 4 5 6 7 8 9 ` | `#1、卸载依赖 yum remove docker-ce docker-ce-cli containerd.io #2、删除资源 rm -rf /var/lib/docker rm -rf /var/lib/containerd 或者直接使用rm -rf /* # /var/lib/docker docker的默认工作路径 ` |
| -------------------- | ------------------------------------------------------------ |
|                      |                                                              |

### 阿里云镜像加速

| `1 2 3 4 5 6 7 8 9 ` | `# 免费可以得到，直接注册阿里云账号就可以从官网得到即可 sudo mkdir -p /etc/docker sudo tee /etc/docker/daemon.json <<-'EOF' {  "registry-mirrors": ["https://e0y63syo.mirror.aliyuncs.com"] } EOF sudo systemctl daemon-reload sudo systemctl restart docker ` |
| -------------------- | ------------------------------------------------------------ |
|                      |                                                              |

### 回顾HelloWorld流程

[![image-20210504214134145](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323292_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323292_0.png)

[![image-20210504220401696](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323741_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323741_0.png)

### 底层原理

**Docker时怎么工作的？**

Docker是一个Client-Server结构的系统，Docker的守护进程运行在主机上，通过Socket从客户端访问，DockerServer接受到Docker-Client的指令，就会执行这个指令

[![image-20210504221117584](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324704_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324704_0.png)

**Docker为什么比VM块？**

1、Docker有着比虚拟机更少的抽象层

2、docker利用的是宿主机的内核，vm需要的是Guest OS

[![image-20210504221322564](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323961_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323961_0.png)

所以说新建一个容器的时候，docker不需要像虚拟机一样去加载一个操作系统内核，避免引导，虚拟机是加载Guest OS，分钟级别的，而docker是利用宿主机的操作系统，省略了复杂的过程，是秒级的

[![image-20210504221754532](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323600_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122323600_0.png)

## Docker的常用命令

### 帮助命令

| `1 2 3 ` | `docker version # 显示docker的版本信息 docker info # 显示docker的系统信息，包括镜像和容器的数量 docker 命令 --help # 帮助命令 ` |
| -------- | ------------------------------------------------------------ |
|          |                                                              |

帮助文档的地址：https://docs.docker.com/engine/reference/commandline/

### 镜像命令

**docker images**查看所有本地主机上的镜像

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 ` | `[root@localhost ~]# docker images REPOSITORY    TAG       IMAGE ID       CREATED       SIZE hello-world   latest    d1165f221234   8 weeks ago   13.3kB #解释 REPOSITORY 镜像的仓库源 TAG		   镜像的标签 IMAGE ID   镜像的id CREATED    镜像的创建时间 SIZE       镜像的大小 # 可选项 --all , -a		# 列出所有镜像 --quiet , -q	# 只显示镜像的id ` |
| --------------------------------------- | ------------------------------------------------------------ |
|                                         |                                                              |







**docker search**搜索镜像

| ` 1 2 3 4 5 6 7 8 9 10 11 12 ` | `[root@localhost ~]# docker search mysql NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED mysql                             MySQL is a widely used, open-source relation…   10823     [OK]        mariadb                           MariaDB Server is a high performing open sou…   4083      [OK]        mysql/mysql-server                Optimized MySQL Server Docker images.  # 可选项 --filter=STARS=3000 # 搜索出来的镜像就是STARS大于3000的 --filter , -f		Filter output based on conditions provided --format		Pretty-print search using a Go template --limit	25	Max number of search results --no-trunc		Don't truncate output ` |
| ------------------------------ | ------------------------------------------------------------ |
|                                |                                                              |

**docker pull**下载镜像

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 ` | `# 下载镜像 docker pull 镜像名[:tag] [root@localhost ~]# docker pull mysql Using default tag: latestn # 如果不写tag，默认是latest latest: Pulling from library/mysql f7ec5a41d630: Pull complete # 分层下载，docker image 的核心，联合文件系统 9444bb562699: Pull complete  6a4207b96940: Pull complete  181cefd361ce: Pull complete  8a2090759d8a: Pull complete  15f235e0d7ee: Pull complete  d870539cd9db: Pull complete  493aaa84617a: Pull complete  bfc0e534fc78: Pull complete  fae20d253f9d: Pull complete  9350664305b3: Pull complete  e47da95a5aab: Pull complete  Digest: sha256:04ee7141256e83797ea4a84a4d31b1f1bc10111c8d1bc1879d52729ccd19e20a # 签名 Status: Downloaded newer image for mysql:latest docker.io/library/mysql:latest # 真实地址 # 等价于它 docker pull mysql docker pull docker.io/library/mysql:latest # 指定版本下载 [root@localhost ~]# docker pull mysql:5.7 5.7: Pulling from library/mysql f7ec5a41d630: Already exists  9444bb562699: Already exists  6a4207b96940: Already exists  181cefd361ce: Already exists  8a2090759d8a: Already exists  15f235e0d7ee: Already exists  d870539cd9db: Already exists  cb7af63cbefa: Pull complete  151f1721bdbf: Pull complete  fcd19c3dd488: Pull complete  415af2aa5ddc: Pull complete  Digest: sha256:a655529fdfcbaf0ef28984d68a3e21778e061c886ff458b677391924f62fb457 Status: Downloaded newer image for mysql:5.7 docker.io/library/mysql:5.7 ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

[![image-20210504225144719](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324296_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324296_0.png)

**docker rmi**删除镜像

| `1 2 3 ` | `[root@localhost ~]# docker rmi -f 87eca374c0ed   # 删除指定的奖项 [root@localhost ~]# docker rmi -f 镜像id1 镜像id2 镜像id3  # 删除多个奖项 [root@localhost ~]# docker rmi -f $(docker images -aq)  # 删除全部镜像 ` |
| -------- | ------------------------------------------------------------ |
|          |                                                              |

### 容器命令

说明：有了镜像才能创建容器，linux，下载一个centos镜像来测试学习

| `1 ` | `docker pull centos ` |
| ---- | --------------------- |
|      |                       |

新建容器再启动

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 ` | `docker run [可选参数] image # 参数说明 --name="name" 容器名字 tomcat01 tomcat02 用来区分容器 -d            后台方式运行 -it           使用交互方式运行 -p            指定容器的端口 -p 8080:8080 -p ip:主机端口:容器端口 -p 主机端口:容器端口（常用） -p 容器端口 容器端口 -P            随机指定端口 # 测试,启动并进入容器 [root@localhost ~]# docker run -it centos /bin/bash [root@021e303bcf9c /]# ls  # 查看容器内的centos基础版本，很多命令都是不完善的 bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var # 从容器中退回主机 [root@021e303bcf9c /]# exit  exit [root@localhost ~]# ls anaconda-ks.cfg  initial-setup-ks.cfg  公共  模板  视频  图片  文档  下载  音乐  桌面 ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

**列出所有运行的容器**

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 ` | `# docker ps 命令   # 列出当前正在运行的容器 -a # 当前正在运行的容器+历史运行过的容器 -n=? # 显示最近创建的容器 -q # 只显示容器的编号 [root@localhost ~]# docker ps CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES [root@localhost ~]# docker ps -a CONTAINER ID   IMAGE          COMMAND       CREATED        STATUS                    PORTS     NAMES 021e303bcf9c   centos         "/bin/bash"   19 hours ago   Exited (0) 19 hours ago             zealous_lamport 22670b1c561e   d1165f221234   "/hello"      20 hours ago   Exited (0) 20 hours ago             magical_euclid ` |
| --------------------------------- | ------------------------------------------------------------ |
|                                   |                                                              |

**退出容器**

| `1 2 ` | `exit # 直接容器停止并退出 Ctrl + P + Q # 容器不停止退出 ` |
| ------ | ---------------------------------------------------------- |
|        |                                                            |

**删除容器**

| `1 2 3 ` | `docker rm 容器id #删除指定容器，不能删除正在运行的容器 docker rm -f $(docker ps -aq) # 删除所有容器 docker ps -a -q|xargs docker rm # 删除所有容器 ` |
| -------- | ------------------------------------------------------------ |
|          |                                                              |

**启动和停止容器的操作**

| `1 2 3 4 ` | `docker start 容器id # 启动容器 docker restart 容器id # 重启容器 docker stop 容器id # 停止当前正在运行的容器 docker kill 容器id # 强制停止当前容器 ` |
| ---------- | ------------------------------------------------------------ |
|            |                                                              |

### 常用其他命令

**后台启动容器**

| `1 2 3 4 5 6 7 ` | `# 命令 docker run -d 镜像名 [root@localhost ~]# docker run -d centos # 问题是docker ps停止了centos # 常见的坑：docker容器使用后台运行就必须要有一个前台进程，容器发现没有应用，就会自动停止 # nginx，容器启动后，发现自己没有提供服务，就会立刻停止，就是没有程序了 ` |
| ---------------- | ------------------------------------------------------------ |
|                  |                                                              |

**查看日志**

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 ` | `docker logs -f -t --tail 容器id  # 自己编写一段shell脚本 [root@localhost ~]# docker run -d centos /bin/sh -c "while true;do echo eric;sleep 1;done" [root@localhost ~]# docker ps CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES 4f95779df41b   centos    "/bin/sh -c 'while t…"   3 seconds ago   Up 3 seconds             nostalgic_edison # 显示日志 -tf # 显示日志 --tail [number] # 要显示的日志条数 [root@localhost ~]# docker logs -f -t --tail 10 4f95779df41b  ` |
| ------------------------------------ | ------------------------------------------------------------ |
|                                      |                                                              |

**查看容器中的进程信息ps**

| `1 2 3 4 5 6 7 ` | `# 命令 docker top 容器id [root@localhost ~]# docker top 4f95779df41b UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD root                10225               10205               0                   18:30               ?                   00:00:00            /bin/sh -c while true;do echo eric;sleep 1;done root                10607               10225               0                   18:34               ?                   00:00:00            /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 1 ` |
| ---------------- | ------------------------------------------------------------ |
|                  |                                                              |

**查看镜像元数据**

| `1 2 3 ` | `# 命令 docker inspect 容器id [root@localhost ~]# docker inspect 4f95779df41b ` |
| -------- | ------------------------------------------------------------ |
|          |                                                              |

**进入当前正在运行的容器**

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 ` | `# 我们通常容器都是在后台运行，需要进入容器，修改一些配置 # 命令 docker exec -it 容器id bashshell [root@localhost ~]# docker ps CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES 4f95779df41b   centos    "/bin/sh -c 'while t…"   10 minutes ago   Up 10 minutes             nostalgic_edison [root@localhost ~]# docker exec -it 4f95779df41b /bin/bash [root@4f95779df41b /]# ls bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var # 方式二 dcoker attach 容器id # 测试 [root@localhost ~]# docker attach dce7bshk8oou7 正在执行当前的代码... docker exec #济泺路容器后开启一个新的终端 docker attach # 进入容器正在执行的终端，不会启动新的进程 ` |
| ------------------------------------------------------ | ------------------------------------------------------------ |
|                                                        |                                                              |

**从容器内拷贝文件到主机上**

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 ` | `docker cp 容器id:容器内路径  目的主机路径 # 查看当前主机目录下 [root@localhost home]# ls eric [root@localhost home]# touch eric.java [root@localhost home]# ls eric  eric.java [root@localhost home]# docker ps CONTAINER ID   IMAGE     COMMAND       CREATED              STATUS              PORTS     NAMES 2ae552528a84   centos    "/bin/bash"   About a minute ago   Up About a minute             sleepy_kowalevski # 进入docker容器内部 [root@localhost home]# docker attach 2ae552528a84 [root@2ae552528a84 /]# cd /home [root@2ae552528a84 home]# ls # 在容器内部进行创建文件 [root@2ae552528a84 home]# touch test.java [root@2ae552528a84 home]# exit exit [root@localhost home]# docker ps -a CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS                     PORTS     NAMES 2ae552528a84   centos    "/bin/bash"   3 minutes ago   Exited (0) 6 seconds ago             sleepy_kowalevski # 见文件拷贝出来到主机上 [root@localhost home]# docker cp 2ae552528a84:/home/test.java /home [root@localhost home]# ls eric  eric.java  test.java # 拷贝是一个手动过程，未来我们可以使用-v卷的技术，可以实现自动同步 /home /home ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

学习方式：将所有命令全部敲一遍

### 小结

[![image-20210505190814029](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324221_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324221_0.png)

### 常用命令总结

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 ` | `  attach      # 当前shell下attach连接指定运行镜像  build       # 通过DockerFile定制镜像  commit      # 提交当前容器为新的镜像  cp          # 从容器中拷贝指定文件或者目录到宿主机中  create      # 创建一个洗掉了容器，通run，但是不启动容器  diff        # 查看docker容器变化  events      # 从docker服务获取容器实时事件  exec        # 在已存在的容器上运行命令  export      # 导出容器的内容流作为一个tar归档文件[对应import]  history     # 展示一个镜像形成历史  images      # 列出系统当前镜像  import      # 从tar包的内容创建一个新的文件系统镜像[对应export]  info        # 显示系统相关信息  inspect     # 查看容器详细信息  kill        # kill指定docker容器  load        # 从一个tar报中加载一个镜像[对应save]  login       # 注册或者登录一个docker源服务器  logout      # 从当前Docker registry退出  logs        # 输出当前容器日志信息  pause       # 暂停容器  port        # 查看映射端口对应的容器内部源端口  ps          # 列出容器列表  pull        # 从docker镜像源服务器拉取指定镜像或者库镜像  push        # 推送指定镜像或者库镜像至docker源服务器  rename      # 重命名容器  restart     # 重启运行的容器  rm          # 移除一个或者多个容器  rmi         # 移除一个或者多个镜像[无容器使用经相关ian个才可以进行删除，否则需要删除相关内容才可以继续或者-f强制删除]  run         # 创建一个新的容器并运行一个命令  save        # 保存一个镜像为一个tar包  search      # 在docker hub中搜索镜像  start       # 启动容器  stats       # 显示容器资源使用统计信息的实时流  stop        # 停止容器  tag         # 给源中镜像打标签  top         # 查看容器中运行的进程信息  unpause     # 取消暂停容器  update      # 更新容器配置  version     # 查看容器版本  wait        # 截取容器停止时的状态值 ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

### 作业练习

> 安装ngnix

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 ` | `# 1、搜索镜像 [root@localhost home]# docker search nginx # 2、拉取镜像 [root@localhost home]# docker pull nginx # 3、查看镜像 [root@localhost home]# docker images REPOSITORY   TAG       IMAGE ID       CREATED        SIZE nginx        latest    62d49f9bab67   3 weeks ago    133MB centos       latest    300e315adb2f   4 months ago   209MB # 4、启动运行 [root@localhost home]# docker run -d --name nginx01 -p 3344:80 nginx 66f84ea1a1679cc5f062e4c7aab26f051d30df710e23e7685597257933eb7d61 # 5、查看运行情况 [root@localhost home]# docker ps CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES 66f84ea1a167   nginx     "/docker-entrypoint.…"   31 seconds ago   Up 29 seconds   0.0.0.0:3344->80/tcp, :::3344->80/tcp   nginx01 # -d 后台运行 # --name 给容器起名字 # -p 宿主机端口:容器内部端口 # 6、本机自测运行情况 [root@localhost home]# curl localhost:3344  Welcome to nginx!     body {        width: 35em;        margin: 0 auto;        font-family: Tahoma, Verdana, Arial, sans-serif;    }  Welcome to nginx! If you see this page, the nginx web server is successfully installed and working. Further configuration is required. For online documentation and support please refer to [nginx.org](http://nginx.org/).  Commercial support is available at [nginx.com](http://nginx.com/). Thank you for using nginx.  # 7、进入容器，修改配置 [root@localhost home]# docker exec -it nginx01 /bin/bash root@66f84ea1a167:/# whereis nginx nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx root@66f84ea1a167:/# cd /etc/nginx root@66f84ea1a167:/etc/nginx# ls conf.d	fastcgi_params	koi-utf  koi-win  mime.types  modules  nginx.conf  scgi_params	uwsgi_params  win-utf root@66f84ea1a167:/etc/nginx#  ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

端口暴露的概念

[![image-20210505195207334](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324083_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324083_0.png)

思考问题：我们每次都需要改动nginx配置，都需要进入容器内部？十分的麻烦，我们要是可以在容器外部提供一个映射路径，达到可以在容器外部修改文件名，容器内部就可以进行自动修改？**-v数据卷**

> 作业：使用docker安装一个tomcat

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 ` | `# 官方使用 docker run -it --rm tomcat:9.0 # 我们之前的启动都是后台，停止了容器之后，容器还是可以查到 docker run -it --rm一般用来测试，用完就删除 # 下载再启动 docker pull tomcat # 启动运行 [root@localhost home]# docker run -d -p 3355:8080 --name tomcat01 tomcat # 访问测试没有问题 # 进入容器 [root@localhost ~]# docker exec -it tomcat01 /bin/bash # 发现问题：1、Linux命令少量 2、没有webapps  阿里云镜像的原因，默认是最小的镜像，所有不必要的都剔除掉，保证最小可运行的环境 ` |
| --------------------------------------------- | ------------------------------------------------------------ |
|                                               |                                                              |

思考问题：如果每次部署都要进入容器是不是非常麻烦？我们要是可以在容器外部提供一个映射路径，webapps，我们在外部防止项目，就自动同步到内部就好了

> 作业：部署es+kibana

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 ` | `# es 暴露的端口非常多 # es十分占用内存 # es的数据一般需要放置在安全目录下，挂载 # --net somenetwork ？ 网络配置 # 启动elasticsearch docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2 # 启动了非常卡  docker stats 查看cpu的状态 # 测试一下es是否成功 [root@localhost ~]# curl localhost:9200 {  "name" : "b0c8c6a0ecc7",  "cluster_name" : "docker-cluster",  "cluster_uuid" : "dNqDoDZpTESGYiO5iGEJJA",  "version" : {    "number" : "7.6.2",    "build_flavor" : "default",    "build_type" : "docker",    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",    "build_date" : "2020-03-26T06:34:37.794943Z",    "build_snapshot" : false,    "lucene_version" : "8.4.0",    "minimum_wire_compatibility_version" : "6.8.0",    "minimum_index_compatibility_version" : "6.0.0-beta1"  },  "tagline" : "You Know, for Search" } # 赶紧关闭，增加内存的限制 ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

[![image-20210505224411116](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324558_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324558_0.png)

| `1 2 3 4 ` | `# 赶紧关闭，增加内存的限制，修改配置文件 -e 环境配置修改 docker run -d --name elasticsearch02 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2 # 查看 docker stats ` |
| ---------- | ------------------------------------------------------------ |
|            |                                                              |

[![image-20210505224845032](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325083_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325083_0.png)

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 ` | `[root@localhost ~]# curl localhost:9200 {  "name" : "b14c3112dbac",  "cluster_name" : "docker-cluster",  "cluster_uuid" : "0ZmORVwIQF6XG3Hc9m57Ng",  "version" : {    "number" : "7.6.2",    "build_flavor" : "default",    "build_type" : "docker",    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",    "build_date" : "2020-03-26T06:34:37.794943Z",    "build_snapshot" : false,    "lucene_version" : "8.4.0",    "minimum_wire_compatibility_version" : "6.8.0",    "minimum_index_compatibility_version" : "6.0.0-beta1"  },  "tagline" : "You Know, for Search" } ` |
| --------------------------------------------------- | ------------------------------------------------------------ |
|                                                     |                                                              |

如何使用kibana连接es?思考网络如何才能连接过去！

[![image-20210505225459036](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324773_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324773_0.png)

### 可视化

- portainer（先用着）
- Rancher(CI/CD再用)

**什么是portainer？**

Docker图形化界面管理工具，提供一个后台面板进行操作

| `1 ` | `docker run -d -p 8088:9000 \--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer ` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

通过它来进行访问：http://222.20.40.100:8088/

可以看到的可视化面板，平时一般不会使用

[![image-20210505231237376](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324319_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324319_0.png)

## Docker镜像讲解

### 镜像是什么

镜像是一种轻量级、可执行的独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需的所有内容，包括代码、运行时、库、环境变量和配置文件。

所有的应用，直接打包docker镜像，就可以直接跑起来

如何得到镜像：

- 从远程仓库下载
- 朋友拷贝给你
- 自己制作一个镜像DockerFile

### Docker镜像加载原理

> UnionFS（联合文件系统）

UnionFS（联合文件系统）：Union文件系统（UnionFS）是一种分层、轻量级并且高性能的文件系统，它支持对文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtual filesystem)。Union 文件系统是 Docker 镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。

特性：一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录。

> 镜像加载原理

bootfs(boot file system)主要包含bootloader和kernel, bootloader主要是引导加载kernel, Linux刚启动时会加载bootfs文件系统，在Docker镜像的最底层是bootfs。这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。

rootfs (root file system)，在bootfs之上。包含的就是典型 Linux 系统中的 /dev,/proc,/bin,/etc 等标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu，Centos等等。

平时我们安装虚拟机的centos都是好几个G，为什么Docker这里才200M？

[![image-20210506121438793](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324386_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324386_0.png)

对于一个精简的OS，rootfs 可以很小，只需要包含最基本的命令，工具和程序库就可以了，因为底层直接用Host的kernel，自己只需要提供rootfs就可以了。由此可见对于不同的linux发行版, bootfs基本是一致的,rootfs会有差别,因此不同的发行版可以公用bootfs。

虚拟机是分钟级别的，容器是秒级别的。

### 分层理解

> 分层的镜像

我们去下载一个镜像，注意观察下载的日志输出，可以看到是一层一层的在下载！

[![image-20210506142415950](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324308_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324308_0.png)

思考：为什么要采用这种分层的结构呢？

最大的好处，我觉得莫过于是资源共享了，比如有多个镜像都从相同的Base镜像构建而来，那么宿主机只需要在磁盘上保留一份base镜像，同时内存中只需要加载一份base镜像，这样就可以为多有的容器服务了，而且每一层都可以被共享

查看镜像分层的方式可以通过docker image inspect 命令

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 ` | `[root@localhost ~]# docker image inspect redis:latest "RootFS": {            "Type": "layers",            "Layers": [                "sha256:7e718b9c0c8c2e6420fe9c4d1d551088e314fe923dce4b2caf75891d82fb227d",                "sha256:89ce1a07a7e4574d724ea605b4877f8a73542cf6abd3c8cbbd2668d911fa5353",                "sha256:9eef6e3cc2937e452b2325b227ca28120a70481be25404ed9aad27fa81219fd0",                "sha256:ee748697d275b904f1d5604345d70b647a8c145b9f05aeb5ca667e1f256e43d8",                "sha256:f1f7964d40afa49c6ef63ab11af91044e518a2539f567783ce997d3cea9ce8f6",                "sha256:3d9fda8ff875e549d54e9d7504ce17d27423fe27dafbb92127c603dddad7fa13"            ]        }, ` |
| ------------------------------------ | ------------------------------------------------------------ |
|                                      |                                                              |

**理解：**

所有的 Docker|镜像都起始于一个基础镜像层，当进行修改或增加新的内容时，就会在当前镜像层之上，创建新的镜像层。

举一个简单的例子，假如基于 Ubuntu Linux 16.04 创建一个新的镜像，这就是新镜像的第一层；如果在该镜像中添加 Python包，就会在基础镜像层之上创建第二个镜像层；如果继续添加一个安全补丁，就会创建第三个镜像层。

该镜像当前已经包含 3 个镜像层，如下图所示（这只是一个用于演示的很简单的例子）。

[![image-20210506144010853](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324557_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324557_0.png)

在添加额外的镜像层的同时，镜像始终是保持当前所有镜像的组合，理解这一点是非常重要的。下图拒了一个简单的例子，每个镜像包含三个文件，而镜像包含了来自两个镜像层的6个文件。

[![img](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325695_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325695_0.png)

上图中的镜像层和之前的图中略有区别，主要目的是便于展示文件

下图中展示了一个稍微复杂的三层镜像，在外部看来整个镜像只有6个文件，这是因为最上层的文件7是文件5的一个更新版

[![image-20210506151545247](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325196_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325196_0.png)

这种情况下，上层镜像层中的文件覆盖了底层镜像层中的文件。这样就使得文件的更新版本作为一个新镜像层添加到镜像当中。 Docker 通过存储引擎（新版本采用快照机制）的方式来实现镜像层堆栈，并保证多镜像层对外展示为统一的文件系統。 Linux 上可用的存储引擎有 AUFS、Overlay2、Device Mapper、Btrfs 以及 ZFS。顾名思义，每种存储引擎都基于 Linux 中对应的文件系统或者块设备技术，并且每种存储引擎都有其独有的性能特点。

Docker 在 Windows 上仅支持 windowsfiter一种存储引擎，该引擎基于 NTFS 文件系统之上实现了分层和 CoW[1]。

下图展示了与系统显示相同的三层镜像。所有镜像层堆叠并合井，对外提供统一的视图。

[![image-20210506152155309](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325109_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325109_0.png)

> 特点

Docker镜像都是只读的，当容器启动时，一个新的可写层被加载到镜像顶部！

这一层就是我们通常说的容器层，容器之下的都叫镜像层

[![image-20210506153603573](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325270_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325270_0.png)

### commit镜像

| `1 2 3 4 ` | `docker commit 提交容器成为一个新的副本 # 命令和git原理类似 docker commit -m="提交的描述信息" -a="作者" 容器id 目标镜像名:[tag] ` |
| ---------- | ------------------------------------------------------------ |
|            |                                                              |

实战测试

| ` 1 2 3 4 5 6 7 8 9 10 11 12 ` | `# 启动一个默认的tomcat # 发现这个默认的tomcat是没有webapps应用的，镜像的原因：官方镜像默认webapps下面没有文件的！ # 我自己拷贝进去了基本的文件 # 将我们自己操作过后的容器通过commit提交为一个镜像，我们以后就可以使用自己修改过的镜像，这就是我们自己的一个修改过的镜像 [root@localhost ~]# docker commit -a="eric" -m="add webapps application" 6f4fd55369bb tomcat02:1.0 sha256:a3eec2c2487fdc97ca6adeecb21d5e02e7ba7501a561256528ba7efb9021d228 # 查看修改过后的镜像 ` |
| ------------------------------ | ------------------------------------------------------------ |
|                                |                                                              |

[![image-20210506203844240](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324950_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324950_0.png)

学习方式说明：理解概念，但是一定要实践，最后实践和理论相结合一次搞定这个知识

| `1 ` | `如果你想要保存当前的状态，就通过commit提交，获得一个镜像，就好比我们以前学习VM时候，快照 ` |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

到了这里才算是入门Docker

## 容器数据卷

### 什么是容器数据卷

**docker的理念回顾**

将应用环境打包成一个镜像！

数据？如果数据都在容器中，那么我们容器删除，数据就会丢失！**需求：数据可以持久化**

MySQL，容器删除了，删库跑路！**需求：MySQL的数据可以存储在本地**

容器之间可以有一个数据共享的技术！docker容器中产生的数据，同步到本地

这就是卷技术，目录的挂载，将容器内的目录挂载在Linux上面

[![image-20210506205536696](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325540_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325540_0.png)

**总结一句话：容器的持久化和同步操作，容器间也是可以数据共享的**

### 使用数据卷

> 方式一：使用命令来挂载 -v

| `1 2 3 4 5 6 ` | `docker run -it -v 主机目录:容器的目录 # 测试 [root@localhost home]# docker run -it -v /home/ceshi:/home centos /bin/bash # 容器启动的时候我们可以通过docker inspect 容器id ` |
| -------------- | ------------------------------------------------------------ |
|                |                                                              |

[![image-20210506210458164](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324893_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324893_0.png)

测试文件的同步

[![image-20210506211128888](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325983_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325983_0.png)

再来测试

1.停止容器

2、宿主机上修改文件

3、启动容器

4、容器内的数据依旧是同步的

[![image-20210506211801910](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325718_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325718_0.png)

好处：我们以后修改只需要在本地进行修改即可，容器内部会自动进行同步！

### 实战：安装MySQL

思考：MySQL的数据持久化问题

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 ` | `# 获取镜像 [root@localhost ~]# docker pull mysql:5.7 # 运行容器，需要做数据挂载，安装MySQL需要配置密码，下面是官方命令 # docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag # 启动我们的 -d 后台运行 -p 端口映射 -v 数据卷挂载 -e 环境配置 --name 容器名字 [root@localhost ~]# docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=338218 --name mysql01 mysql:5.7 # 在启动成功后，我们在本地使用sqlyog来测试连接一下 # sqlyog--连接到服务器3310---3310和容器内部的3306进行映射，这个时候我们就可以连接上了 # 在蹦迪测试新建一个数据库，查看一下我们映射的路径是否ok ` |
| --------------------------------------------------- | ------------------------------------------------------------ |
|                                                     |                                                              |

假设我们删除容器

[![image-20210506214141667](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324550_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122324550_0.png)

发现我们挂载在本地的数据卷依旧没有丢失，这就是容器的持久化功能

### 具名和匿名挂载

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 ` | `# 匿名挂载，注意这里使用-P表示的指定随机的端口号，没有指定主机的位置信息 -v 容器内路径 docker run -d -P --name nginx01 -v /etc/nginx nginx # 查看所有卷的情况 [root@localhost ~]# docker volume ls local     1d0b3ba7045ef37ab30b087687b36325c1941d2178961c23d511a89f38d757aa # 这里发现，这种就是匿名挂载，我们在-v只写了容器内的路径，没有写容器外的路径 # 具名挂载 [root@localhost ~]# docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx nginx 8571cb0d59725be9ab6f9efabcfd2a9d709ff99ceee59348494f567872829a67 [root@localhost ~]# docker volume ls DRIVER    VOLUME NAME local     1d0b3ba7045ef37ab30b087687b36325c1941d2178961c23d511a89f38d757aa local     455e0591eae1c3969b1b8bf82da94c821a8e94c156650b328bf0720498f2dee6 local     juming-nginx # 通过 -v 卷名:容器内路径 # 查看一下这个卷 ` |
| --------------------------------------------------------- | ------------------------------------------------------------ |
|                                                           |                                                              |

[![image-20210506215227961](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325977_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325977_0.png)

所有的docker容器内的卷，在没有指定目录的情况下都是在`/var/lib/docker/volumes/xxx/_data`

我们通过具名挂载可以方便找到我们的一个卷，大多数情况下都是使用`具名挂载`

| `1 2 3 4 ` | `# 如何确定是匿名挂载还是具名挂载，还是指定路径挂载 -v 容器内路径 # 匿名挂载 -v 卷名:容器内路径 # 具名挂载 -v 宿主机路径:容器内路径 # 指定路径挂载 ` |
| ---------- | ------------------------------------------------------------ |
|            |                                                              |

拓展：

| `1 2 3 4 5 6 7 8 9 ` | `# 通过 -v 容器内路径:ro rw 改变读写权限 ro readonly # 只读 rw readwrite # 可读可写 # 一旦设置了这个容器权限，容器对我们挂载出来的内容就有了限定了 docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:ro nginx docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:rw nginx # ro 只要看到ro就说明这个路径只能通过宿主机来操作，容器内部是无法进行操作的 ` |
| -------------------- | ------------------------------------------------------------ |
|                      |                                                              |

### 初识DockerFile

DockerFile就是用来构建docker镜像的构建文件，命令脚本，先体验一下

通过这个脚本可以生成一个镜像，镜像是一层层的，所以脚本是一个个的命令

| ` 1 2 3 4 5 6 7 8 9 10 11 ` | `# 创建一个dockerfile文件，名字可以随机，建议Dockerfile # 文件中的内容 指令（大写） 参数 FROM centos VOLUME ["volume01","volume02"] CMD echo "---end---" CMD /bin/bash # 这里的每个命令就是镜像的一层 ` |
| --------------------------- | ------------------------------------------------------------ |
|                             |                                                              |

[![image-20210506222027144](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325531_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325531_0.png)

[![image-20210506222107630](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325587_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325587_0.png)

| `1 2 ` | `# 启动一下自己写的容器 [root@localhost docker-test-volume]# docker run -it fded8c01a457 /bin/bash ` |
| ------ | ------------------------------------------------------------ |
|        |                                                              |

[![image-20210506222438278](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325760_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325760_0.png)

这个卷和外部一定有一个同步的目录

[![image-20210506222628890](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325857_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325857_0.png)

查看一下卷挂载的路径

| `1 ` | `[root@localhost data]# docker inspect fca535846c94 ` |
| ---- | ----------------------------------------------------- |
|      |                                                       |

[![image-20210506223145866](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325873_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325873_0.png)

测试一下文件是否已经被同步出去了

这种方式未来的使用非常多，因为我们自己通常会构建自己的镜像

假设构建镜像的时候没有挂载，需要自己手动挂载镜像 -v 卷名:容器内路径

### 数据卷容器

多个MySQL同步数据

[![image-20210506224019709](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325762_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325762_0.png)

| `1 ` | `# 启动3个容器，通过我们刚在自己写的镜像启动 ` |
| ---- | ---------------------------------------------- |
|      |                                                |

[![image-20210506230229069](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325491_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325491_0.png)

[![image-20210506231252458](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122326003_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122326003_0.png)

docker01的数据同步到了docker02

[![image-20210506231106013](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325850_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325850_0.png)

[![image-20210506231733375](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325967_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325967_0.png)

| `1 2 ` | `# 测试 ：可以删除容器dcoker01，查看docker02和docker03时候还可以访问这个文件 # 测试结果是依然可以访问到 ` |
| ------ | ------------------------------------------------------------ |
|        |                                                              |

[![image-20210506232522977](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325646_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_122325646_0.png)

多个MySQL实现数据共享

| `1 2 3 4 5 ` | `docker run -d -p 3310:3306 -v /etc/mysql/conf.d -v /var/lib/mysql -e MYSQL_ROOT_PASSWORD=338218 --name mysql01 mysql:5.7 docker run -d -p 3310:3306 -e MYSQL_ROOT_PASSWORD=338218 --name mysql02 --volumes-from mysql01 mysql:5.7 # 这个时候可以实现两个容器数据同步 ` |
| ------------ | ------------------------------------------------------------ |
|              |                                                              |

结论：

容器之间配置信息的传递，数据卷容器的生命周期这一直持续到没有容器使用为止

但是一旦持久化到了本地，这个时候，本地的数据不会被删除

## DockerFile

### DockerFile介绍

dockerfile是用来构建docker镜像的文件，命令参数脚本

构建步骤：

1、编写一个dockerfile文件

2、docker build构建为一个镜像

3、docker run 运行镜像

4、docker push发布镜像（DockerHub、阿里云镜像仓库）

查看一下官方是怎么做的

[![image-20210507154128224](https://gitee.com/eric_bb/image/raw/master/202105/20210507_154128857_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_154128857_0.png)

[![image-20210507154358305](https://gitee.com/eric_bb/image/raw/master/202105/20210507_154358781_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_154358781_0.png)

很多官方的镜像都是基础包，很多功能都没有，我们通常会自己搭建自己的镜像

官方可以制作镜像，那我们也可以

### DockerFile镜像的构建

**基础知识：**

1、每个保留关键字（指令）都是必须是大写字母

2、执行从上到下顺序执行

3、#表示注释

4、每一个指令都会创建提交一个新的镜像层，并提交

[![image-20210507154952005](https://gitee.com/eric_bb/image/raw/master/202105/20210507_155009094_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_155009094_0.png)

dockerfile是面向开发的，我们以后要发布项目，做镜像，就需要编写dockerfile文件，这个文件十分简单！

Docker镜像逐渐成为了企业交付的标准，必须要掌握

步骤：开发，部署，运维…缺一不可

DockerFile：构建文件，定义了一切的步骤，源代码

DockerImages：通过DockerFile构建生成的镜像，最终发布和运行的产品

Docker容器：容器就是镜像运行起来提供服务的

### DockerFile指令

| ` 1 2 3 4 5 6 7 8 9 10 11 12 ` | `FROM  # 基础镜像，一切从这里开始 MAINTAINER # 镜像是谁写的，姓名+邮箱 RUN  # 镜像构建的时候需要运行的命令 ADD  # 步骤：tomcat镜像，这个tomcat压缩包，添加内容 WORKDIR  # 镜像的工作目录 VOLUME  #挂载的目录 EXPOSE  # 暴露端口配置 CMD  # 指定容器运行时的shell命令，只有最后一个生效，可被替代 ENTRYPOINT # 指定容器运行时的shell命令，可以追加命令 ONBUILD  # 当构建一个被继承DockerFile这个还是会就会运行ONBUILD的指令，触发指令 COPY  # 类似ADD，将我们文件拷贝到镜像中 ENV  # 构建的时候设置环境变量 ` |
| ------------------------------ | ------------------------------------------------------------ |
|                                |                                                              |

[![image-20210507155631163](https://gitee.com/eric_bb/image/raw/master/202105/20210507_155631711_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_155631711_0.png)

### 实战测试

Docker Hub中99%的镜像都是从这个基础镜像过来的FROM scratch，然后配置需要的软件和配置来进行构建的

[![image-20210507161057482](https://gitee.com/eric_bb/image/raw/master/202105/20210507_161057961_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_161057961_0.png)

> 创建一个自己的centos

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 ` | `# 1、编写Dockerfile文件 [root@localhost dockerfile]# cat mydockerfile-centos  FROM centos MAINTAINER eric ENV MYPATH /usr/local WORKDIR $MYPATH RUN yum -y install vim RUN yum -y install net-tools EXPOSE 80 CMD echo $MYPATH CMD echo "----end----" CMD /bin/bash # 2、通过这个文件构建镜像 # 命令 docker build -f dockerfile文件路径 -t 镜像名:[tag] Successfully built dc4556607d09 Successfully tagged mycentos:0.1 # 3、测试运行 ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

对比：之前原生的centos

[![image-20210507163437878](https://gitee.com/eric_bb/image/raw/master/202105/20210507_163438394_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_163438394_0.png)

我们增加之后的镜像

[![image-20210507163535804](https://gitee.com/eric_bb/image/raw/master/202105/20210507_163536254_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_163536254_0.png)

我们可以列出本地镜像的变更历史：`docker history 镜像id`

| `1 ` | `[root@localhost ~]# docker history dc4556607d09 ` |
| ---- | -------------------------------------------------- |
|      |                                                    |

[![image-20210507203437483](https://gitee.com/eric_bb/image/raw/master/202105/20210507_203438003_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_203438003_0.png)

### 用实战看CMD和ENTRYPOINT的区别

> CMD和ENTRYPOINT的区别
>
> 通过下面的测试可以看出：
>
> 1、CMD和ENTRYPOINT都可以执行其中的命令
>
> 2、如果在运行的时候追加命令，CMD会报错，而ENTRYPOINT会将追加的命令拼接在其文件中的命令之后，并且会正常运行

| `1 2 ` | `CMD  # 指定容器运行时的shell命令，只有最后一个生效，可被替代 ENTRYPOINT # 指定容器运行时的shell命令，可以追加命令 ` |
| ------ | ------------------------------------------------------------ |
|        |                                                              |

**测试cmd**

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 ` | `# 1、编写Dockerfile文件 [root@localhost dockerfile]# vim dockerfile-cmd-test # 2、查看Dockerfile文件内容 [root@localhost dockerfile]# cat dockerfile-cmd-test  FROM centos CMD ["ls","-a"] # 3、通过文件构建镜像 [root@localhost dockerfile]# docker build -f dockerfile-cmd-test -t cmdtest . Sending build context to Docker daemon  3.072kB Step 1/2 : FROM centos ---> 300e315adb2f Step 2/2 : CMD ["ls","-a"] ---> Running in 66de685aea90 Removing intermediate container 66de685aea90 ---> 8c2ead017eb2 Successfully built 8c2ead017eb2 Successfully tagged cmdtest:latest # 4、通过run运行，可以看出会执行ENTRYPOINT ["ls","-a"]中的ls -a命令 [root@localhost dockerfile]# docker run 8c2ead017eb2 . .. .dockerenv bin dev etc home lib lib64 lost+found media mnt opt proc root run sbin srv sys tmp usr var # 想追加命令-l ls -al，会出现错误 [root@localhost dockerfile]# docker run 8c2ead017eb2 -l docker: Error response from daemon: OCI runtime create failed: container_linux.go:367: starting container process caused: exec: "-l": executable file not found in $PATH: unknown. ERRO[0000] error waiting for container: context canceled  # cmd的清理下-l替换了CMD["ls","-a"]命令，-l不是命令所以报错！ ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

**测试ENTRYPOINT**

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 ` | `# 1、编写Dockerfile文件 [root@localhost dockerfile]# vim dockerfile-cmd-entrypoint # 2、查看Dockerfile文件内容 [root@localhost dockerfile]# cat dockerfile-cmd-entrypoint  FROM centos ENTRYPOINT ["ls","-a"] # 3、通过文件构建镜像 [root@localhost dockerfile]# docker build -f dockerfile-cmd-entrypoint -t entrypoint-test . Sending build context to Docker daemon  4.096kB Step 1/2 : FROM centos ---> 300e315adb2f Step 2/2 : ENTRYPOINT ["ls","-a"] ---> Running in ac9565897497 Removing intermediate container ac9565897497 ---> 9519aeef7394 Successfully built 9519aeef7394 Successfully tagged entrypoint-test:latest # 4、通过run运行，可以看出会执行CMD ["ls","-a"]中的ls -a命令 [root@localhost dockerfile]# docker run 9519aeef7394 . .. .dockerenv bin dev etc home lib lib64 lost+found media mnt opt proc root run sbin srv sys tmp usr var # 想追加命令-l，直接拼接，变成 ls -al，可以正常运行 [root@localhost dockerfile]# docker run 9519aeef7394 -l total 0 drwxr-xr-x.   1 root root   6 May  7 13:07 . drwxr-xr-x.   1 root root   6 May  7 13:07 .. -rwxr-xr-x.   1 root root   0 May  7 13:07 .dockerenv lrwxrwxrwx.   1 root root   7 Nov  3  2020 bin -> usr/bin drwxr-xr-x.   5 root root 340 May  7 13:07 dev drwxr-xr-x.   1 root root  66 May  7 13:07 etc drwxr-xr-x.   2 root root   6 Nov  3  2020 home lrwxrwxrwx.   1 root root   7 Nov  3  2020 lib -> usr/lib lrwxrwxrwx.   1 root root   9 Nov  3  2020 lib64 -> usr/lib64 drwx------.   2 root root   6 Dec  4 17:37 lost+found drwxr-xr-x.   2 root root   6 Nov  3  2020 media drwxr-xr-x.   2 root root   6 Nov  3  2020 mnt drwxr-xr-x.   2 root root   6 Nov  3  2020 opt dr-xr-xr-x. 295 root root   0 May  7 13:07 proc dr-xr-x---.   2 root root 162 Dec  4 17:37 root drwxr-xr-x.  11 root root 163 Dec  4 17:37 run lrwxrwxrwx.   1 root root   8 Nov  3  2020 sbin -> usr/sbin drwxr-xr-x.   2 root root   6 Nov  3  2020 srv dr-xr-xr-x.  13 root root   0 May  4 12:33 sys drwxrwxrwt.   7 root root 145 Dec  4 17:37 tmp drwxr-xr-x.  12 root root 144 Dec  4 17:37 usr drwxr-xr-x.  20 root root 262 Dec  4 17:37 var ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

### 实战：Tomcat镜像

**1、准备镜像文件，tomcat**

[![image-20210507212501939](https://gitee.com/eric_bb/image/raw/master/202105/20210507_212502405_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_212502405_0.png)

**2、编写dockerfile文件，文件命名为`Dockerfile`，就不需要-f去指定了，build会自动寻找这个文件**

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 ` | `FROM centos MAINTAINER eric COPY readme.txt /usr/local/readme.txt ADD jdk-8u221-linux-x64.tar.gz /usr/local/ ADD apache-tomcat-9.0.45.tar.gz /usr/local/ RUN yum -y install vim ENV MYPATH /usr/local WORKDIR $MYPATH ENV JAVA_HOME /usr/local/jdk1.8.0_221 ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.45 ENV CATALINA_BASH /usr/local/apache-tomcat-9.0.45 ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin EXPOSE 8080 CMD /usr/local/apache-tomcat-9.0.45/bin/startup.sh && tail -F /usr/local/apache-tomcat-9.0.45/bin/logs/catalina.out ` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
|                                                              |                                                              |

**3、构建镜像**

| `1 2 ` | `# 注意，不能掉了最后一个点'.' [root@localhost tomcat]# docker build -t diytomcat . ` |
| ------ | ------------------------------------------------------------ |
|        |                                                              |

**4、启动镜像**

| `1 2 3 4 5 6 7 8 ` | `[root@localhost tomcat]# docker run -d -p 9090:8080 --name erictomcat -v /home/eric/build/tomcat/test:/usr/local/apache-tomcat-9.0.45/webapps/test -v /home/eric/build/tomcat/tomcatlogs/:/usr/local/apache-tomcat-9.0.45/logs diytomcat # 解释，第一个挂载是将webapps下的test映射到本地tomcat下的test -v /home/eric/build/tomcat/test:/usr/local/apache-tomcat-9.0.45/webapps/test # 解释，第二个挂载是将apache-tomcat-9.0.45下的日志映射到本地tomcat下的tomcatlogs -v /home/eric/build/tomcat/tomcatlogs/:/usr/local/apache-tomcat-9.0.45/logs  ` |
| ------------------ | ------------------------------------------------------------ |
|                    |                                                              |

**5、访问测试**

访问http://222.20.40.100:9090/，可以看到成功的界面

[![image-20210507221203626](https://gitee.com/eric_bb/image/raw/master/202105/20210507_221204203_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_221204203_0.png)

**6、发布项目**（由于做了卷挂载，我们直接在本地编写项目就可以发布了）

在本地`tomcat/test`文件夹下创建`WEB-INF`文件夹，在`WEB-INF`下编写`web.xml`文，在`/test` 下编写`index.jsp`文件，再访问http://222.20.40.100:9090/test/

| `1 2 3 4 5 6 7 8 ` | `      ` |
| ------------------ | -------- |
|                    |          |

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 ` | `<%@ page language="java" contentType="text/html; charset=UTF-8"    pageEncoding="UTF-8"%> <%@ page import="java.io.*,java.util.*, javax.servlet.*" %>  hello,eric  显示当前时间与日期 <%   Date date = new Date();   out.print( "" +date.toString()+""); %>  ` |
| --------------------------------------------- | ------------------------------------------------------------ |
|                                               |                                                              |

可以看到成功访问的页面

[![image-20210507221348837](https://gitee.com/eric_bb/image/raw/master/202105/20210507_221349305_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_221349305_0.png)

我们以后的开发步骤：需要掌握Dockerfile的编写，我们之后的一切都是使用docker镜像来发布运行！

### 发布自己的镜像

> Docker Hub

**1、地址https://hub.docker.com/**

**2、注册账号，确定这个账号可以登录**

**3、登录服务器**

| ` 1 2 3 4 5 6 7 8 9 10 11 12 13 14 ` | `# 查看相关的登录命令，必须先登录才能提交上去 [root@localhost tomcat]# docker login --help Usage:  docker login [OPTIONS] [SERVER] Log in to a Docker registry. If no server is specified, the default is defined by the daemon. Options:  -p, --password string   Password      --password-stdin    Take the password from stdin  -u, --username string   Username ` |
| ------------------------------------ | ------------------------------------------------------------ |
|                                      |                                                              |

| `1 2 3 4 5 6 7 8 9 ` | `# 使用docker login -u [用户名]，然后输入密码就可以登录成功 [root@localhost tomcat]# docker login -u ericbooney Password:  WARNING! Your password will be stored unencrypted in /root/.docker/config.json. Configure a credential helper to remove this warning. See https://docs.docker.com/engine/reference/commandline/login/#credentials-store Login Succeeded ` |
| -------------------- | ------------------------------------------------------------ |
|                      |                                                              |

**4、登录完毕后就可以提交上去镜像，就是一步 docker push**

| ` 1 2 3 4 5 6 7 8 9 10 11 12 ` | `# 这里提交出现了错误，因为需要在diytomcat前面加上自己docker hub的username [root@localhost tomcat]# docker push diytomcat Using default tag: latest The push refers to repository [docker.io/library/diytomcat] a8724fc7877e: Preparing  39a8a3af5dab: Preparing  b0a26c702c9b: Preparing  7560bca74509: Preparing  2653d992f4ef: Preparing  denied: requested access to the resource is denied ` |
| ------------------------------ | ------------------------------------------------------------ |
|                                |                                                              |

**一定要修改diytomcat的镜像名字为ericbooney/diytomcat，所以为了避免出现错误，在build的时候就要在名称前面加上自己docker hub的用户名**

| `1 2 3 ` | `# 修改diytomcat为ericbooney/diytomcat:1.0，也尽量带上版本号 [root@localhost tomcat]# docker tag diytomcat ericbooney/diytomcat:1.0 ` |
| -------- | ------------------------------------------------------------ |
|          |                                                              |

| `1 2 3 4 5 6 7 8 9 ` | `# 再次进行提交，可以看到成功提交 [root@localhost tomcat]# docker push ericbooney/diytomcat:1.0 Using default tag: latest The push refers to repository [docker.io/ericbooney/diytomcat] a8724fc7877e: Pushed  39a8a3af5dab: Pushed  b0a26c702c9b: Pushing [==================================>                ]  277.3MB/406.7MB 7560bca74509: Pushed  2653d992f4ef: Pushed  ` |
| -------------------- | ------------------------------------------------------------ |
|                      |                                                              |

### 小结

[![image-20210507230305076](https://gitee.com/eric_bb/image/raw/master/202105/20210507_230305611_0.png)](https://gitee.com/eric_bb/image/raw/master/202105/20210507_230305611_0.png)

## Docker网络

文章作者 Eric

上次更新 2021-05-07

[Docker](https://eric_bb.gitee.io/tags/docker/)

[背包九讲 ](https://eric_bb.gitee.io/post/背包九讲/)

<iframe title="livereAd" scrolling="no" frameborder="0" src="https://was.livere.me/ad?consumerSeq=1020&amp;livereSeq=53152&amp;isMobile=false&amp;site=http://eric_bb.gitee.io/post/docker/&amp;uuid=45328b22-3023-46c6-9a3d-0c702c0b34bb" id="lv-ad-174" style="min-width: 100%; width: 100px; height: 0px; overflow: visible; border: 0px; z-index: 124212;"></iframe>

由 [Hugo](https://gohugo.io/) 强力驱动 | 主题 - [Even](https://github.com/olOwOlo/hugo-theme-even)

本站总访问量 514 次 | 本站总访客数 113 人

© 2021Eric