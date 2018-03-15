# LNMP
LNMP环境搭建(附带WNMP)

//Uye
1.查看CentOS版本（OS7及以上可能部分命令无效）
cat /etc/redhat-release

2.关掉防火墙（测试环境使用）
# service iptables stop 
# chkconfig iptables off

3.配置更新yum源
# yum update // 更新源
# yum install epel-release // 扩展包更新包
# vi /etc/yum.repos.d/nginx.repo // 添加nginx官方源
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
4.安装开发包和库文件
# yum install ntp make openssl openssl-devel pcre pcre-devel libpng libpng-devel libjpeg-6b libjpeg-devel-6b freetype freetype-devel gd gd-devel zlib zlib-devel gcc gcc-c++ libXpm libXpm-devel ncurses ncurses-devel libmcrypt libmcrypt-devel libxml2 libxml2-devel imake autoconf automake screen sysstat compat-libstdc++-33 curl curl-devel

<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
5.如果已经有安装httpd mysql php nginx等可以执行操作（慎重！！！！）操作前务必确保数据备份至最新
# yum remove httpd
# yum remove mysql
# yum remove php
# yum remove nginx
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

6.安装nginx
# yum install nginx
# chkconfig --levels 235 nginx on // 设2、3、5级别开机启动
# service nginx start

7.安装mysql
#
  yum install mysql mysql-server mysql-devel
  chkconfig --levels 235 mysqld on // 设2、3、5级别开机启动
  service mysqld start
#

8.安装PHP
# rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
# yum install php70w lighttpd-fastcgi php70w-cli php70w-gd php70w-imap php70w-ldap php70w-odbc php70w-pear php70w-xml php70w-xmlrpc php70w-mbstring php70w-mcrypt php70w-mssql php70w-snmp php70w-soap php70w-tidy php70w-common php70w-devel php70w-fpm php70w-mysql
// 安装php和所需组件使PHP支持MySQL、FastCGI模式
# chkconfig --levels 235 php-fpm on // 设2、3、5级别开机启动
# service php-fpm start

9.配置nginx支持PHP
# 配置文件拷贝/替换，nginx.conf fcgi.conf
# 完全开放nginx配置端口

10.安装memcached
# yum install –enablerepo=rpmforge memcached libevent libevent-devel
# wget https://launchpad.net/libmemcached/1.0/1.0.18/+download/libmemcached-1.0.18.tar.gz
# tar -zxf libmemcached-1.0.18.tar.gz
# cd libmemcached-1.0.18/
# ./configure
# make && make install
# git clone https://github.com/php-memcached-dev/php-memcached.git
# cd php-memcached/
# git checkout php7
# phpize
# ./configure --disable-memcached-sasl
# make && make install
# vim /etc/php.ini
# 末行增加 
[Memcached]
extension=memcached.so
# service php-fpm restart	
# chkconfig --level 2345 memcached on // 设2、3、5级别开机启动
# service memcached start

11.安装redis
# yum install redis
# git clone https://github.com/phpredis/phpredis.git
# cd phpredis
# git checkout php7
# phpize
# ./configure
# make && make install
# vim /etc/php.ini
# 末行增加
[Redis]
extension=redis.so
# service php-fpm restart
# chkconfig --level 2345 redis on // 设2、3、5级别开机启动
# service redis start
