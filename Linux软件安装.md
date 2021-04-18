# Linux软件安装  
---
## 1. rpm包的管理
+ 介绍  
  rpm用于互联网下载包的打包及安装工具，它包含在某些Linux分发版中。它生成具有 *.rpm* 扩展名的文件。rpm是**RedHat Package Manager**（RedHat软件包管理工具）的缩写，类似于Windows的setup.exe，这一文件格式名称虽然打上了RedHat的标志，但理念是通用的。Linux的分发版本都有采用（SUSE，RedHat，CentOS等等），可以算是公认的行业标准
+ rpm包的简单查询指令  
  `rpm -qa | grep xx`查询已安装的特定rpm包
+ rpm包的基本格式  
  *firefox-60.2.2-1.el7.centos.x86_64*  
  名称：firefox  
  版本号：60.2.2-1  
  适用操作系统：el7-centos.x85_64（表示CentOS7.x的64位系统，如果是i686、i386表示32位系统，noarch表示通用）  
+ rpm包的其他查询指令
  `rpm -qa`&emsp;查询所安装的所有rpm包  
  `rpm -qa | more`&emsp;  
  `rpm -qa | grep xx`&emsp;  
  `rpm -qa 软件包名`&emsp;查询软件包是否安装  
  `rpm -qi 软件报名`&emsp;查询软件包信息  
  `rpm -qf 文件路径`&emsp;查询文件所属的软件包  
  `rpm -e 软件包名`&emsp;卸载rpm包（如果其他软件包依赖于这个软件包，卸载时回产生错误信息）  
  `rpm -e --nodeps 软件包名`&emsp;忽略错误信息强制卸载（可能会导致其他软件包失去依赖无法使用）  
  `rpm -ivh rpm包路径`&emsp;安装软件包（*-i*安装，*-v*提示，*-h*进度条）  
---
## 2. yum
+ 基本介绍  
  yum是一个Shell前端软件包管理器，基于rpm包管理，能从指定服务器自动下载rpm包并且安装。可以自动处理依赖性关系，并且一次安装所有依赖的软件包  
+ yum的基本指令  
  `yum list | grep xx软件列表`&emsp;查询yum服务器是否有需要安装的软件  
  `yum install xxx`&emsp;下载安装
---
## 3. 安装JavaEE开发所需要的软件
+ 概述，如果需要在Linux下进行JavaEE的开发，需要安装如下软件：
  + *ideaIU.2020.2.3.tar.gz*
  + *apache-tomcat-8.5.59.tar.gz*
  + *mysql-5.7.26-1-el7.x86.64.rpm-bundle.tar*
  + *jdk-8u261-linux-x64.tar.gz*
  + *CentOS-7-x86_64-DVD-1810.iso*
+ JDK8.0安装步骤
  1. 创建解压目录`mkdir /opt/jdk`  
  2. 通过xftp将 *jdk-8u261-linux-x64.tar.gz* 上传到 *opt/jdk* 目录下  
  3. `cd /opt/jdk`  
  4. 解压文件`tar -zxvf jdk-8u261-linux-x64.tar.gz`  
  5. 创建安装目录`mkdir /usr/local/java`  
  6. 将解压后的文件移动到安装目录`mv /opt/jdk/jdk1.8.0_261 /ussr/local/java`  
  7. 修改环境变量的配置文件`vim /etc/profile`  
  8. 在文件最后插入`export JAVA_HOME=/usr/local/java/jak1.8.0_261`和`export PATH=$JAVA_HOME/bin:$PATH`，保存退出  
  9.  输入`source /etc/profile`使配置文件生效  
+ tomcat安装步骤
  1. 创建解压目录`mkdir /opt/tomcat`  
  2. 通过xftp将 *apache-tomcat-8.5.59.tar.gz* 上传到 *opt/tomcat* 目录下  
  3. `cd /opt/tomcat`  
  4. 解压文件`tar -zxvf apache-tomcat-8.5.59.tar.gz`  
  5. 进入解压目录 */bin* ，启动tomcat`./startup.sh`  
  6. 开启端口8080`firewall-cmd --permanent --add-port=8080/tcp`，并重载`firewall-cmd --reload`  
+ IDEA2020的安装
  1. 进入官网下载IDEA Linux版文件  
  2. 创建解压目录`mkdir /opt/idea`  
  3. 通过xftp将 *ideaIU.2020.2.3.tar.gz* 上传到 *opt/idea* 目录下  
  4. 启动 *bin/* 目录下`./idea.sh`文件，配置JDK
+ MySQL安装步骤
  1. 创建解压目录`mkdir /opt/mysql`  
  2. 运行`wget http://dev.mysql.com/get/mysql-5.7.26-1-el7.x86.64.rpm-bundle.tar`下载MySQL安装包  
  3. 运行`tar -xvf mysql-5.7.26-1-el7.x86.64.rpm-bundle.tar`  
  4. 由于CentOS7.6自带有类MySQL数据库**MariaDB**，会跟MySQL产生冲突，所以需要先删除，运行`rpm -qa | grep mariadb`查询是否有MariaDB相关安装包，如果有运行`rom -e --nodeps mariadb-libs`卸载  
  5. 依次执行`rpm -ivh mysql-community-common-5.7.26-1.el7.x86_64.rpm`、`rpm -ivh mysql-community-libs-5.7.26-1.el7.x86_64.rpm`、`rpm -ivh mysql-community-client-5.7.26-1.el7.x86_64.rpm`、`rpm -ivh mysql-community-server-5.7.26-1.el7.x86_64.rpm`  
  6. 运行`ststemctl start mysqld.service`启动MySQL服务  