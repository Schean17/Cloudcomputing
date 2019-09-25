# CentOS 7安装Docker

- 已安装CentOS 7，并且内核版本大等于3.10，本文使用的是阿里云的镜像：[CentOS镜像](http://mirrors.aliyun.com/centos/7/isos/x86_64/)。
- 非root用户已获得sudo特权。

使用如下命令查看操作系统内核信息：

```
uname -r
```

结果如图所示：

![1569381919548](README.assets/1569381919548.png)

顺带看一下Linux的版本号：

```
cat /etc/redhat-release

```

结果如图所示

![1569381970779](README.assets/1569381970779.png)



安装Docker依赖包

```
yum install -y yum-utils device-mapper-persistent-data lvm2 
```

![1569382157970](README.assets/1569382157970.png)

![1569382171422](README.assets/1569382171422.png)



设置阿里云镜像

```
 yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo 
```

![1569382590803](README.assets/1569382590803.png)



### 安装 Docker-CE

```
yum install docker-ce
```

![1569382731246](README.assets/1569382731246.png)

![1569382697380](README.assets/1569382697380.png)



安装完成之后设置开机启动并启动Docker守护进程，即Docker服务：

```
systemctl enable docker
 systemctl start docker
```

![1569382789469](README.assets/1569382789469.png)



验证Docker是否成功启动：

```
sudo systemctl status docker
```

![1569382832437](README.assets/1569382832437.png)



此外，还可以查看一下Docker的版本信息：

```
docker version

```

输出如图：

![1569382903742](README.assets/1569382903742.png)