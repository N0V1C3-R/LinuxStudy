# Linux网络配置  
---
## 1. 网络环境配置
+ 方式一：自动获取
  + 说明
    登录后，通过界面来设置自动获取IP
  + 特点
    Linux启动后会自动获取IP，缺点是每次自动获取的IP地址可能不一样
+ 方式二：指定IP
  + 说明
    直接修改配置文件来指定IP，并可以连接到外网
  + 操作步骤
    1. 使用`vi /etc/sysconfig/network-scripts/ifcfg-ens33`命令修改*ifcfg-ens33*文件来配置IP  
    2. *ifcfg-ens33*文件修改
        >TYPE="Ethernet"  
        PROXY_METHOD="none"  
        BROWSER_ONLY="no"  
        #IP的配置方法none | static | bootp | dhcp  
        #引导时不使用协议 | 静态分配IP | BOOTP协议 | DHCP协议  
        BOOTPROTO="dhcp"--------->BOOTRPOTO="static"  
        DEFROUTE="yes"  
        IPV4_FAILURE_FATAL="no"  
        IPV6INIT="yes"  
        IPV6_AUTOCONF="yes"  
        IPV6_DEFROUTE="yes"  
        IPV6_FAILURE_FATAL="no"  
        IPV6_ADDR_GEN_MODE="stable-privacy"  
        NAME="ens33"  
        UUID="81fd32f9-c339-4d38-8949-3ce851ed6e4d"  
        DEVICE="ens33"  
        ONBOOT="yes"  
        #添加设置IP地址
        IPADDR=192.168.168.168
        #添加设置网关  
        GATEWAY=192.168.168.66  
        #添加设置域名解析器  
        DNS1=192.168.168.66
    3. 修改虚拟机中虚拟网络配置器的对应子网IP和网关  
    4. 重启网络服务`service network`或重启系统`reboot`  
---
## 2. 设置主机名和hosts映射
+ 为什么要设置主机名？
  之前我们都是根据IP来记忆主机，但在实际生产中往往不会这么记忆，所以为了方便生产和开发，可以给Linux系统设置主机名，也可以根据需要修改主机名
+ 设置主机名
  1. 指令`hostname`查看主机名  
  2. 修改 */etc/hostname* 文件指定主机名  
  3. 修改完成后重启系统生效  
+ 设置hosts映射
  + 如何通过主机名找到（比如ping）某个Linux系统？
    + windows
      在 *C:\Windows\System32\drivers\etc\hosts* 文件指定  
      案例：192.168.168.168 N2M
    + Linux
      在 */etc/hosts* 文件指定  
      案例：192.168.168.66 Windows
+ 主机名解析过程（Hosts、DNS）
  + Hosts是什么
    + 一个文本文件，用来记录IP和Hostname的映射关系
  + DNS
    1. DNS就是 *Domain Name System* 的缩写，翻译过来就是域名系统  
    2. 是互联网上作为域名和IP地址相互映射的一个分布式数据库
  + 解析过程
    当主机寻找一个域名的IP时先从浏览器缓存中进行查找，如果浏览器缓存中没有，就从本地Hosts文件查找其对应关系，如果本地Hosts文件中也没有找到，就从DNS服务器中查找，查找方式可以是迭代查询也可以是递归查询（该过程与计算机网络中DNS查询过程相同）