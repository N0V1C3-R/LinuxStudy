# Linux介绍
---
## 1. Linux概述
+ 1.1 Linux是一个开源、免费的操作系统，其稳定性、安全性、处理多并发的能力都被界所认可，许多企业级项目都会部署到Linux/Unix系统上
+ 1.2 常见Linux发行版本：**Ubuntu**、**RedHat**、**CentOS**、**Debian****SUSE**、**Fedora**...
+ 1.3 Linux之父是*Linus Torvalds*（Linux v0.0.1）
---
## 2. Linux和Unix的关系
+ 2.1 Unix是怎么来的？
  >+ 上世纪70年代，贝尔实验室、麻省理工大学、美国通用电气公司想要研发一个多用户分时操作系统*multics*，但项目并未成功
  >+ *Ken Tompson*（B语言、Golang发明者）在**multics**项目基础上进行改进，将其改名为**Unix**（最早版本是用B语言进行编写），*Dennis Richres*与*Ken Tompson*一起将Unix系统改为使用C语言进行编写
  >+ 80年代，许多公司根据Unix操作系统的开源源码对其进行二次开发并发行，著名有Aix（IBM公司）、SOLARIS（Sun公司）、hpUX（HP公司）
  >+ 由于Unix操作系统只能运行在大型的高性能服务器上，一般人不能承担如此高昂代价，此时*Richard Stallman*（号称世界第一黑客，黑客精神领袖）提出：在自时代用户应享有对软件源代码阅读和修改的权力，软件公司可以通过靠提供服务和训获得盈利。于是*Richard Stallman*发起了一个GNU计划，让更多人享受对源代码的用权
+ 2.2 Linux是怎么来的？
  >*Linus Torvalds*在研究生时期加入GNU计划，贡献了**Linux Kernel**内核，后来许多开发者对其进行了改进（所以Linux完整的叫法应该是GNU/Linux)
+ 2.3 Linux和Unix的关系
  >Linux是在**AT&T System V**版本下引申出的**Minix**版本的基础上进行重新改写而来，适用于x86的个人计算机
---
## 3. 安装VMWare和CentOS
+ 3.1 什么是VMWare？
  >+ VMWare是一个虚拟机，通过软件模拟具有完整硬件系统功能的、运行在一个完全隔离环境中的计算机系统，如果没有实体机，CentOS安装在虚拟机上运行
  >+ 下载地址：http://www.vmware.com/cn.html
+ 3.2 VM安装注意事项
  >进入BIOS修改设置开启虚拟化设备支持
+ 3.3 Linux安装分区设置
  >+ /boot分区（一般1G）<br>
  设备类型：标准分区；文件系统：ext4
  >+ swap交换分区（一般与设置的内存分区一致）（临时充当内存）<br>
  设备类型：标准分区；文件系统：swap
  >+ 根分区（分配剩余内存）<br>
  设备类型：标准分区；文件系统：ext4
+ 3.4 Linux安装网络链接三种模式
  >+ 桥接模式<br>
  如果虚拟系统和外部通信，网段必须和主机相同，但由于网段内主机数量有限，容易造成IP冲突
  >+ NAT模式（网络地址转换模式）<br>
  使用NAT模式进行配置，主机会根据虚拟机IP对应的虚拟网卡，主机与虚拟机中间会生成独立可相互通信的网络，虚拟机可以通过主机实际IP代理与外部网络通信，不造成IP冲突
  >+ 主机模式<br>
  独立系统，不与外部联系
+ 3.5 vmtools
  >+ 作用：<br>
  实现Linux虚拟机与Windows操作系统文件共享
  >+ 步骤：
  >   1. 进入CentOS，点击VM菜单：虚拟机->install vmware tools
  >   2. CentOS会出现一个VM的安装包：xx.tar.gz，将安装包拷贝到/opt
  >   3. 打开终端输入命令：
      `cd /opt`   切换到/opt目录
      `tar -zxvf xx.tar.gz`   解压文件
      `cd vmware-wools-distrib/`  切换到解压目录
      `./vmware-install.pl`   安装
---
## 4. 远程登陆使用Linux
+ 4.1 为什么要远程登陆Linux？
  >Linux服务器是开发小组共享的，正式上线的项目是运行在公网上的，因此程序员需要远程登陆到Linux进行项目的管理和开发
+ 4.2 如何远程登陆到Linux？
  >1. 测试设备是否连通<br>
        Linux终端输入`ipconfig`查找ens33设备IP地址<br>
        Windows终端输入`ping 所查找到的IP地址`<br>
        如果有数据传输说明设备联通
  >2. 使用远程登录软件输入IP地址建立连接
  >3. 登陆账号
+ 4.3 远程上传下载文件
  >1. 使用远程文件传输软件输入IP地址
  >2. 传输协议使用SFTP，端口号为22
  >3. 登录账号建立连接
+ 4.4 中文乱码问题
  >编码方式改为UTF-8