机器测试 
-
    wget -qO- bench.sh | bash
  
speedtest终端测速
-

      git clone https://github.com/sivel/speedtest-cli.git 安装测速脚本
      cd speedtest-cli        cd脚本
      python speedtest.py    运行测速
      
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



