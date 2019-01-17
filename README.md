# Review-Board

最近打算研究一下开源的code review 工具，然后网上查找一番，打算自己搭建一下Review Board记录一下    

## 1、好像需要python环境，Centos 系统中一些命令会依赖Python，因此系统会默认安装Python。如果为Centos 7，Python版本为 2.7.5，无需重新安装，可以通过以下命令检查。    

python – version    

![Image 下载文件](https://github.com/liweiDiao/Review-Board/blob/master/images/1.png)    

## 2、安装 MySQL    

1. 添加MySQL Yum 仓库    
   wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm     
   输入命令出现（wget: 未找到命令）的错误，输入：  yum -y install wget     没有错误请忽视！    
  ![Image 下载文件](https://github.com/liweiDiao/Review-Board/blob/master/images/2.png)    
  
2. 安装RPM包     
  rpm -Uvh mysql57-community-release-el7-11.noarch.rpm    
  ![Image 下载文件](https://github.com/liweiDiao/Review-Board/blob/master/images/3.png)  

3. 使用 yum 安装 mysql-community-server     
  yum install mysql-community-server    
  
4. 启动MySQL服务     
  service mysqld start    

5. 初始化 MySQL
  (1. 生成临时密码 
  grep ‘temporary password’ /var/log/mysqld.log
  
  ![Image 下载文件](https://github.com/liweiDiao/Review-Board/blob/master/images/4.png) 

  (2. 使用临时密码登录MySQL 
  mysql -u root -p

  (3. 修改root用户的密码为“root” 
  ALTER USER ‘root’@’localhost’ IDENTIFIED BY ‘root123456’;
  
6. 修改 MySQL 字符集
  (1. 修改 /etc/my.cnf文件，添加character-set-server=utf8 
  vi /etc/my.cnf

  (2. 重启mysqld服务，重新登录MySQL，验证是否生效 
  service mysqld restart

  (3. 登录MySQL 
  mysql –u root –p

  (4. Show variables like‘character%’;
  
  ![Image 下载文件](https://github.com/liweiDiao/Review-Board/blob/master/images/5.png) 
 
# 3、安装 Apache Web服务器
  1. 使用yum安装httpd 
  yum install httpd

![Image 下载文件](https://github.com/liweiDiao/Review-Board/blob/master/images/6.png) 

  2. 添加httpd为系统服务 
  systemctl enable httpd.service

  3. 安装 Apache HTTP服务器的mod_wsgi 拓展模块（支持使用了Python WSGI标准的Python应用） 
  yum install mod_wsgi

  4. 启动 httpd 服务 
  service httpd start
 
 # 4、安装 ReviewBoard
  1. 添加EPEL安装包数据源 
  yum install epel-release

  2. 安装 memcached ，为ReviewBoard提供缓存服务 
  yum install memcached

  3. 安装 ReviewBoard 
  yum install ReviewBoard

 
  
