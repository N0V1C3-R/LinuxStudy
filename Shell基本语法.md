# Shell基本语法
---
## 1. 条件判断
+ 基本语法  
  `[ codition ]`（注意condition前后一定要有空格）（非空返回true，可使用$?验证） 
+ 判断语句
  + 常用判断条件
    1. `=`字符串比较
    2. 两个整数的比较
       2.1 `-lt`小于  
       2.2 `-le`小于等于  
       2.3 `-eq`等于  
       2.4 `-gt`大于  
       2.5 `-ge`大于等于  
       2.6 `-ne`不等于  
    3. 按照文件权限进行判断  
       3.1 `-r`有读权限  
       3.2 `-w`有写权限  
       3.3 `-x`有执行权限  
    4. 按照文件类型进行判断
       4.1 `-f`文件存在并且是一个常规文件  
       4.2 `-e`文件存在  
       4.3 `-d`文件存在并且是一个目录
+ 应用实例
  ```Shell
    #!/bin/bash
    #案例一："ok"是否等于"ok"
    if [ "ok" = "ok" ]
    then
        echo "equal"
    fi

    #案例二：23是否大于等于22
    if [ 23 -ge 22 ]
    then
        echo "大于"
    fi

    #案例三：/root/shcode/aaa.txt 目录中的文件是否存在
    if [ -f /root/shcode/aaa.txt ]
    then
        echo "存在"
    fi

    if [  ]
    then
        echo "为假"
    fi

    if [ 123 ]
    then
        echo "hello"
    fi
  ```
  执行输出：  
  ```
  equal
  大于
  hello
  ```
---
## 2. 流程控制
+ if判断
  + 基本语法
    ```Shell
    #单分支
    if [ 条件判断式 ]
    then
        代码
    fi

    #多分支
    if [ 条件判断式 ]
    then
        代码
    elif [ 条件判断式 ]
    then
        代码
    fi
    ```
  + 案例
    输入命令：  
    `vim ifCase.sh`  
    编写Shell脚本：
    ```Shell
    #!/bin/bash
    #案例：编写一个Shell程序，如果输入的参数大于等于60，输出“及格了”，如果小于60则输出“不及格”
    if [ $1 -ge 60 ]
    then
        echo "及格了"
    elif [ $1 -lt 60 ]
    then
        echo "不及格"
    fi
    ```
    执行脚本：  
    `chmod u+x ifCase.sh`  
    `./ifCase.sh 50`  
    执行结果:
    ```
    不及格
    ```
+ case语句
  + 基本语法
    ```Shell
    case $变量名 in
    "值1")
        如果变量值等于值1，执行程序1
    ;;
    "值2")
        如果变量值等于值2，执行程序2
    ;;
    ...省略其他分支...
    *)
        如果变量值都与以上情况不服，执行程序
    ;;
    esac
    ```
  + 案例
    输入命令：  
    `vim caseTest.sh`  
    编写Shell脚本：
    ```Shell
    #!/bin/bash
    #案例：编写一个Shell程序，如果输入的参数是1，输出“周日”，如果是6输出“周六”，其他情况输出“老老实实上班吧”
    case $1 in
    "1")
        echo "周日"
    ;;
    "6")
        echo "周六"
    ;;
    *)
        echo "老老实实上班吧"
    ;;
    esac
    ```
    执行脚本：  
    `chmod u+x caseTest.sh`  
    `./ifCase.sh 1`  
    执行结果:
    ```
    周日
    ```
+ for循环
  + 基本语法
    ```Shell
    #语法一：
    for 变量 in 值1 值2 值3...
    do
    程序/代码
    done

    #语法二：
    for (( 初始值;循环控制条件;变量变化 ))
    do
    程序
    done
    ```
  + 案例
    输入命令：  
    `vim forTest.sh`  
    编写Shell脚本：
    ```Shell
    #!/bin/bash
    #案例一：打印命令行输入的参数[这里可以看出$*和$@的区别]
    #注意$*是把输入的参数当作一个整体，所以只会输出一句
    for i in "$*"
    do
        echo "num os $i"
    done
    echo "============================="
    #使用$@来获取输入的参数，注意：这时是分别对待的，所以有几个参数，就输出几句
    for j in "$@"
    do
        echo "num is $j"
    done

    echo "============================="
    #案例二：从1加到100的值
    #定义一个变量SUM
    SUM=0
    for (( m=1; i<=100; i++ ))
    do
        SUM=$[$SUM+$m]
    done
    echo "总和SUM=$SUM"
    ```
    执行脚本：  
    `chmod u+x forTest.sh`  
    `./forTest.sh 100 200 300`  
    执行结果:
    ```
    num is 100 200 300
    =============================
    num is 100
    num is 200
    num is 300
    =============================
    总和SUM=5050
    ```
+ while循环
  + 基本语法
    ```Shell
    #语法一：
    while [ 条件判断式 ]
    do
        程序/代码
    done
    ```
  + 案例
    输入命令：  
    `vim whileTest.sh`  
    编写Shell脚本：
    ```Shell
    #!/bin/bash
    #案例一：从命令行输入一个数n，统计从1+...+n的值
    SUM=0
    i=0
    while [ $i -le $1 ]
    do
        SUM=$[$SUM+$i]
        #i自增
        i=$[$i+1]
    done
    echo "执行结果=$SUM"
    ```
    执行脚本：  
    `chmod u+x whileTest.sh`  
    `./forTest.sh 100`  
    执行结果:
    ```
    执行结果=5050
    ```
---
## 3. read读取控制台输入
+ 基本语法
  `read [选项] [参数]`
+ 常用选项
  *-p*：指定读取值时的提示符  
  *-t*：指定读取是等待的时间（秒），如果没有在指定的时间内输入就不再等待
+ 参数
  指定读取值的变量名
+ 案例
  输入命令：  
  `vim readTest.sh`  
  编写Shell脚本：
  ```Shell
  #!/bin/bash
  #案例一：读取控制台输入的一个NUM1
  read -p "请输入NUM1=" NUM1
  echo "你输入的NUM1=$NUM1"

  #案例一：读取控制台输入的一个NUM2，在10秒内输入
  read -t 10 -p "请输入一个数NUM2" NUM2
  echo "你输入的NUM1=$NUM2"
  ```
  执行脚本：  
  `chmod u+x whileTest.sh`  
  `./whileTest.sh`  
---
## 4. 函数
+ 基本介绍
  Shell编程和其他编程语言一样，有系统函数，也可以自定义函数
+ 系统函数
  + **basename**
    + 基本功能  
        用于返回完整路径最后/的部分，常用于获取文件名  
    + 基本语法  
        `basename [pathname] [suffix]`&ensp;basename命令会删掉所有浅醉包括最后一个'/'字符，然后将字符串显示出来，suffix为后缀，如果suffix被置顶了，basename会将pathname或string中的suffix去掉  
    + 举例：返回 */home/aaa/test.txt* 的 **test.txt** 部分  
        `basename /home/aaa/test.text`
  + **dirname**
    + 基本功能  
        用于返回完整路径最后/的前面部分，常用于返回路径部分  
    + 基本语法  
        `dirname abspath`&emsp;从给定的包含绝对路径的文件名中去除文件名（非目录部分），然后返回剩下的路径  
    + 举例：返回 */home/aaa/test.txt** 的 **/home/aaa** 部分
        `dirname /home/aaa/test.txt`
+ 自定义函数
  + 基本语法
    ```Shell
    function funname[()]
    {
        Action;
        [return int;]
    }
    ```
    调用直接写函数名:`funname [值]`
  + 案例
     输入命令：  
    `vim funTest.sh`  
    编写Shell脚本：
    ```Shell
    #!/bin/bash
    #案例一：：计算输入两个参数的和（动态获取），函数名为getSum
    #定义函数
    function getSum() {
        SUM=$[$n1+$n2]
        echo "结果=$SUM"
    }

    #输入两个值
    read -p "请输入一个值n1=" n1
    read -p "请输入一个值n2=" n2

    #调用自定义函数
    getSum $n1 $n2
    ```
    执行脚本：  
    `chmod u+x funTest.sh`  
    `./funTest.sh`  
## 5. Shell编程综合案例
+ 需求分析
  1. 每天凌晨两点2:30备份数据库 *N2MDB* 到 */data/backup/db*  
  2. 备份开始和备份结束能够给出相应的提示信息  
  3. 备份后的文件要求以备份时间为文件名，并打包成 *.tar.gz* 的形式，比如：2021-04-18_095003.tar.gz  
  4. 在备份的同时，检查是否有10天前备份的数据库文件，如果有就将其删除  
+ 操作步骤  
  `cd /usr/sbin`切换到root用户目录下进行脚本编写  
  `vim mysql_db_backup.sh`创建并编写Shell脚本文件  
  ```Shell
  #!/bin/bash
  #备份目录
  BACKUP=/data/backup/db
  #获取当前时间
  DATETIME=$(date +%Y-%m-%d_%H%M%S)
  #数据库的地址
  HOST=localhost
  #数据库用户名
  DB_USER=root
  #数据库密码
  DB_PWD=123456
  #备份的数据库
  DATABASE=N2MDB

  #创建备份目录：如果目录不存在就创建
  [ ! -d "${BACKUP}/${DATETIME}" ] && mkdir -p "${BACKUP}/${DATETIME}"

  #备份数据库
  mysqldump -u${DB_USER} -p${DB_PWD} --host=${HOST} -q -R --databases ${DATABASE} | gzip > ${BACKUP}/${DATETIME}/$DATETIME.sql.gz

  #将文件处理成.tar.gz
  cd ${BACKUP}
  tar -zcvf $DATETIME.tar.gz ${DATETIME}
  #删除对应的备份目录
  rm -rf ${BACKUP}/${DATITIME}

  #删除10天前的备份文件
  find ${BACKUP} -atime +10 -name "*.tar.gz" -exec rm -rf {} \;
  echo "备份数据库${DATABASE}完成"
  ```
  `crondtab -e`编辑进程调度
  ```
  30 2 * * * /usr/sbin/mysql_db_backup.sh
  ```