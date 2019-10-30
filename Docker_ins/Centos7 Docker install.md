# Centos7 Docker install



## step 1 先置配置



![image-20191029165756858](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029165756858.png)

查看内核版本

![image-20191029165806583](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029165806583.png)

**添加用户到wheel组中（默认拥有sudo权限）**

![image-20191029165813431](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029165813431.png)



## 安装Docker

**更新yum程序数据库**

![image-20191029171439847](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029171439847.png)

**安装Docker依赖**

![image-20191029171702039](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029171702039.png)



**设置阿里云镜像**

![image-20191029171849946](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029171849946.png)



**安装Docker-ce**

![image-20191029172059729](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029172059729.png)



**启动Docker**

![image-20191029172420627](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029172420627.png)



**查看运行状态**

```
sudo systemctl status docker
```

![image-20191029172451451](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029172451451.png)



**设置开机启动**

```
sudo systemctl enable docker
```

![image-20191029172627465](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029172627465.png)



**查看Docker版本信息**

```
sudo docker version
```

![image-20191029172931686](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029172931686.png)

[^错误提醒]: 不加sudo会有些权限无法显示

![image-20191029172745953](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029172745953.png)





## 加载Docker镜像



![image-20191029175725773](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029175725773.png)





![image-20191029175843026](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029175843026.png)





![image-20191029180029554](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029180029554.png)





![image-20191029180038841](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029180038841.png)





## 运行Docker容器



![image-20191029180121193](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029180121193.png)





![image-20191029181047744](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029181047744.png)

  - ```
    Failed to synchronize cache for repo 'BaseOS', ignoring this repo.
    Error: 
      Problem: conflicting requests
    
    - nothing provides /etc/mime.types needed by httpd-2.4.37-12.module_el8.0.0+185+5908b0db.x86_64
    - nothing provides libbrotlienc.so.1()(64bit) needed by httpd-2.4.37-12.module_el8.0.0+185+5908b0db.x86_64
      (try to add '--skip-broken' to skip uninstallable packages or '--nobest' to use not only best candidate packages)
    ```




设置开机启动



![image-20191029201200299](Centos7 Docker install.assets/image-20191029201200299.png)

## 创建新的镜像

退出当前容器

![image-20191029181353798](C:\Users\ikutarian\AppData\Roaming\Typora\typora-user-images\image-20191029181353798.png)

查看本地容器

![image-20191029181524777](Centos7 Docker install.assets/image-20191029181524777.png)



创建一个新的容器



 sudo docker commit -m "add apache web" -a “ll” 03e9d463e632 test_repository/centos-apache-web


![image-20191029182102080](Centos7 Docker install.assets/image-20191029182102080.png)



![image-20191029192346896](Centos7 Docker install.assets/image-20191029192346896.png)



![image-20191029192736479](Centos7 Docker install.assets/image-20191029192736479.png)



更改tag

sudo docker tag [your container's IMAGE ID] [docker-hub-user-name]/[repository-name]:[TAG]

![image-20191029193254732](Centos7 Docker install.assets/image-20191029193254732.png)



## 推送到远程仓库

docker login -u [docker-username]


![image-20191029193650567](Centos7 Docker install.assets/image-20191029193650567.png)



![image-20191029195058021](Centos7 Docker install.assets/image-20191029195058021.png)

sudo docker push [Repository] :[tag]






![image-20191029195518410](Centos7 Docker install.assets/image-20191029195518410.png)



## 在容器中安装Wordpress

打开安装了httpd的容器

![image-20191029195746681](Centos7 Docker install.assets/image-20191029195746681.png)



systemctl start httpd.service


 System has not been booted with systemd as init system (PID 1). Can't operate. Failed to conn

![image-20191029200209328](Centos7 Docker install.assets/image-20191029200209328.png)



sudo docker run -it -p 2222:22 -p 8888:80 4fceeaf878e6 /bin/bash



sudo docker run -d -it --privileged --name wordpress -p 8888:80 -d 4fceeaf878e6 /usr/sbin/init


![image-20191029205838692](Centos7 Docker install.assets/image-20191029205838692.png)

![image-20191029205958601](Centos7 Docker install.assets/image-20191029205958601.png)

安装mysql



![image-20191029210805573](Centos7 Docker install.assets/image-20191029210805573.png)

![image-20191029210939372](Centos7 Docker install.assets/image-20191029210939372.png)



安装php

 yum install epel-release yum-utils
 yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm

![image-20191029214906332](Centos7 Docker install.assets/image-20191029214906332.png)



![image-20191029214929789](Centos7 Docker install.assets/image-20191029214929789.png)

![image-20191029215036379](Centos7 Docker install.assets/image-20191029215036379.png)



![image-20191029215237478](Centos7 Docker install.assets/image-20191029215237478.png)



![image-20191029222617944](Centos7 Docker install.assets/image-20191029222617944.png)



![image-20191029222559553](Centos7 Docker install.assets/image-20191029222559553.png)





容器里无wget，无git，无rsync工具，需手动下载（centos8版本）



![image-20191029232427755](Centos7 Docker install.assets/image-20191029232427755.png)



![image-20191029232610275](Centos7 Docker install.assets/image-20191029232610275.png)





提交带有wordpress的容器

![image-20191029233103944](Centos7 Docker install.assets/image-20191029233103944.png)

![image-20191029233227149](Centos7 Docker install.assets/image-20191029233227149.png)



更改tag

![image-20191029233428512](Centos7 Docker install.assets/image-20191029233428512.png)





### 推送到远程仓库



![image-20191029234202791](Centos7 Docker install.assets/image-20191029234202791.png)