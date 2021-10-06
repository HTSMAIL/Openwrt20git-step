机器测试 
-
    wget -qO- bench.sh | bash
  
speedtest终端测速
-

      git clone https://github.com/sivel/speedtest-cli.git 
      cd speedtest-cli        
      python speedtest.py    
      
移动文件
-

    (1)将/usr/udt中的所有文件移到当前目录(用”.”表示)中：
      $ mv /usr/udt/* .
      
    (2)将文件test.txt重命名为wbk.txt：
      $ mv test.txt wbk.txt

（3）把当前目录的一个子目录里的文件移动到另一个子目录里

       mv  文件名/*  另一个目录

（4）移动当前文件夹下的所有文件到上一级目录

       mv * ../
       
文件或文件夹的复制命令
-

1.cp命令

    cp dir1/a.doc dir2 表示将dir1下的a.doc文件复制到dir2目录下

    cp -r dir1 dir2 表示将dir1及其dir1下所包含的文件复制到dir2下

    cp -r dir1/. dir2 表示将dir1下的文件复制到dir2,不包括dir1目录

    说明：cp参数 -i：询问，如果目标文件已经存在，则会询问是否覆盖；

2.scp命令

    例如：scp id_rsa.pub router_17@IP:/home/router_17/.ssh/authorized_keys可以实现将A电脑上的pub文件拷贝到B电脑上某个位置。
    同cp一样，如果复制的是整个文件夹的内容，则应使用scp -r 命令。

3.扩展阅读

    文件移动（mv）

    文件移动不同于文件拷贝，文件移动相当于我们word中的术语剪切和粘贴。

    命令：mv AAA BBB 表示将AAA改名成BBB
    
 4.解压命令
 tar
    解包：tar zxvf filename.tar
    打包：tar czvf filename.tar dirname
gz命令
    解压1：gunzip filename.gz
    解压2：gzip -d filename.gz
    压缩：gzip filename
      .tar.gz 和  .tgz
      解压：tar zxvf filename.tar.gz
      压缩：tar zcvf filename.tar.gz dirname
      压缩多个文件：tar zcvf filename.tar.gz dirname1 dirname2 dirname3.....
bz2命令
    解压1：bzip2 -d filename.bz2
    解压2：bunzip2 filename.bz2
    压缩：bzip2 -z filename
        .tar.bz2

       解压：tar jxvf filename.tar.bz2
       压缩：tar jcvf filename.tar.bz2 dirname
bz命令
      解压1：bzip2 -d filename.bz
      解压2：bunzip2 filename.bz
         .tar.bz
       解压：tar jxvf filename.tar.bz
z命令
      解压：uncompress filename.z
      压缩：compress filename
        .tar.z
          解压：tar zxvf filename.tar.z
          压缩：tar zcvf filename.tar.z dirname
zip命令
    
      解压：unzip filename.zip
      压缩：zip filename.zip dirname
  
系统
-
    
    uname -a               查看内核/操作系统/CPU信息
    lsb_release -a         查看操作系统版本 (适用于所有的linux，包括Redhat、SuSE、Debian等发行版，但是在debian下要安装lsb)   
    cat /proc/cpuinfo      查看CPU信息
    hostname               查看计算机名
    lspci -tv              列出所有PCI设备
    lsusb -tv              列出所有USB设备
    lsmod                  列出加载的内核模块
    env                    查看环境变量

资源
-
    free -m                查看内存使用量和交换区使用量
    df -h                  查看各分区使用情况
    du -sh <目录名>        查看指定目录的大小
    grep MemTotal /proc/meminfo   查看内存总量
    grep MemFree /proc/meminfo    查看空闲内存量
    uptime                 查看系统运行时间、用户数、负载
    cat /proc/loadavg      查看系统负载

磁盘和分区
-

    mount | column -t      查看挂接的分区状态
    fdisk -l               查看所有分区
    swapon -s              查看所有交换分区
    hdparm -i /dev/hda     查看磁盘参数(仅适用于IDE设备)
    dmesg | grep IDE       查看启动时IDE设备检测状况

网络
-

    ifconfig               查看所有网络接口的属性
    iptables -L            查看防火墙设置
    route -n               查看路由表
    netstat -lntp          查看所有监听端口
    netstat -antp          查看所有已经建立的连接
    netstat -s             查看网络统计信息

进程
-

    ps -ef                 查看所有进程
    top                    实时显示进程状态
    
用户
-

    w                      查看活动用户
    id <用户名>            查看指定用户信息
    last                   查看用户登录日志
    cut -d: -f1 /etc/passwd   查看系统所有用户
    cut -d: -f1 /etc/group    查看系统所有组
    crontab -l             查看当前用户的计划任务

服务
-

    chkconfig --list       列出所有系统服务
    chkconfig --list | grep on    列出所有启动的系统服务
    
程序
-

    rpm -qa                查看所有安装的软件包
    

cat指令平时用的最多的主要是在终端查看某个文件
-

1.终端打开文件，查看文件内容。

    cat filename

2.创建一个新文件。

    cat  >  filename

3.将几个文件合并为一个文件。

    cat   file1   file2  > file

 

语法格式：

    cat [-AbeEnstTuv] [--help] [--version] fileName
参数说明：

    -n 或 --number：由 1 开始对所有输出的行数编号。

    -b 或 --number-nonblank：和 -n 相似，只不过对于空白行不编号。

    -s 或 --squeeze-blank：当遇到有连续两行以上的空白行，就代换为一行的空白行。

    -v 或 --show-nonprinting：使用 ^ 和 M- 符号，除了 LFD 和 TAB 之外。

    -E 或 --show-ends : 在每行结束处显示 $。

    -T 或 --show-tabs: 将 TAB 字符显示为 ^I。

    -A, --show-all：等价于 -vET。

    -e：等价于"-vE"选项；

    -t：等价于"-vT"选项；


