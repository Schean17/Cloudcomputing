# 在CentOs上配置WordPress



## 1.安装Apache Web服务器

使用yum工具安装：

sudo yum install httpd

sudo命令获得了root用户的执行权限，因此需要验证用户口令。
安装完成之后，启动Apache Web服务器：

sudo systemctl start httpd.service

测试Apache服务器是否成功运行，找到腾讯云实例的公有IP地址(your_cvm_ip)，在你本地主机的浏览器上输入：

http://your_cvm_ip/

若运行正常，将出现如下界面：





## 2.安装MySQL

CentOS 7.2的yum源中并末包含MySQL，需要其他方式手动安装。因此，我们采用MySQL数据库的开源分支MariaDB作为替代。
安装MariaDB：

sudo yum install mariadb-server mariadb
1
安装好之后，启动mariadb：

sudo systemctl start mariadb
1
随后，运行简单的安全脚本以移除潜在的安全风险，启动交互脚本：

sudo mysql_secure_installation
1
设置相应的root访问密码以及相关的设置(都选择Y)。
最后设置开机启动MariaDB：

sudo systemctl enable mariadb.service
1

## 3.安装PHP

PHP是一种网页开发语言，能够运行脚本，连接MySQL数据库，并显示动态网页内容。
默认的PHP版本太低（PHP 5.4.16），无法支持最新的WordPress（笔者写作时为5.2.2），因此需要手动安装PHP较新的版本(PHP 7.2)。
PHP 7.x包在许多仓库中都包含，这里我们使用Remi仓库，而Remi仓库依赖于EPEL仓库，因此首先启用这两个仓库

sudo yum install epel-release yum-utils
sudo yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
1
2
接着启用PHP 7.2 Remi仓库：

sudo yum-config-manager --enable remi-php72
1
安装PHP以及php-mysql

sudo yum install php php-mysql
1
查看安装的php版本：

php -v
1
安装之后，重启Apache服务器以支持PHP：

sudo systemctl restart httpd.service
1
安装PHP模块
为了更好的运行PHP，需要启动PHP附加模块，使用如下命令可以查看可用模块：

yum search php-
1
部分结果如图所示：



## 4.测试PHP



## 5.安装WordPress以及完成相关配置

### (1)为WordPress创建一个MySQL数据库



### (2)安装WordPress



### (3)配置WordPress



### (4)通过Web界面进一步配置WordPress