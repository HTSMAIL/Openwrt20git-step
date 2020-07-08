# Openwrt20git-step编译步骤究极说明

#  关于虚拟机如何运行 
出处：https://blog.csdn.net/ballack_linux/article/details/81331527

    简述： 由于.img文件没法被vmware直接使用，需要转换成vmdk格式的，那么需要使用qemu-img工具。

    #ubuntu下直接使用 ：    
    sudo  apt-get  install  qemu-utils  -y
    #输入指令
    sudo qemu-img convert -f raw openwrt-xxx.img -O vmdk openwrt-xxx.vmdk

火力全开

     #一键起飞编译方法
    make V=99 -j 96  
