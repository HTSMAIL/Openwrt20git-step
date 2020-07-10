# Openwrt20git-step编译步骤究极说明

#  关于虚拟机如何运行 
出处：https://blog.csdn.net/ballack_linux/article/details/81331527

    简述： 由于.img文件没法被vmware直接使用，需要转换成vmdk格式的，那么需要使用qemu-img工具。

    #ubuntu下直接使用 ：    
    sudo  apt-get  install  qemu-utils  -y
    #输入指令
    sudo qemu-img convert -f raw openwrt-xxx.img -O vmdk openwrt-xxx.vmdk

#改网口地址（默认网关ip）

        vim /etc/config/network

火力全开

     #一键起飞编译方法
    make V=99 -j 96  

# 以lede为例自定义一个自己的专属wrt固件
采用L大的源码，仓库地址
https://github.com/HTSMAIL/lede

#教程内容：
中文：如何编译自己需要的 OpenWrt 固件
-
注意：
-
1. **不**要用 **root** 用户 git 和编译！！！
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.1.1, 密码 password

编译命令如下:
-
1. 首先装好 Ubuntu 64bit，推荐  Ubuntu  18 LTS x64

2. 命令行输入 

        sudo apt-get update 

然后安装依赖输入

       sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf


3. 使用 `git` 命令下载好源代码，然后  进入目录
        
        git clone https://github.com/coolsnowwolf/lede
        cd lede
        vi feeds.conf.default

修改源
推荐下面的软件包，几乎涵盖了你需要插件

```bash
src-git kenzo https://github.com/V2RaySSR/openwrt-packages
src-git small https://github.com/V2RaySSR/small
    ```
        
        备用地址
       src-git https://github.com/HTSMAIL/openwrt-packages
       src-git https://github.com/HTSMAIL/small

        openwrt 固件编译自定义主题与软件
        luci-app-openclash ——————openclash图形
        luci-app-advancedsetting ——————系统高级设置
        luci-theme-atmaterial ——————atmaterial 三合一主题（适配18.06）
        luci-app-aliddns ——————阿里云ddns
        luci-theme-argon-dark-new——————适配19.07与18.06的主题
        luci-app-eqos ——————依IP地址限速
        luci-app-gost ——————隐蔽的https代理
        luci-app-adguardhome ——————去广告
        luci-app-smartdns ——————smartdns防污染
        luci-app-passwall ——————Lienol大神
        luci-theme-argon_new ——————适配19.07与18.06的主题
        luci-app-ssr-plus ——————Lean大神
        luci-theme-opentomcat ——————修复主机名错误（适配18.06）
        luci-theme-opentomato ——————修复主机名错误（适配18.06）

4. ```bash
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
   ```

5.下载dl库（国内请尽量全局科学上网）
        
        make -j8 download V=s
    
        make -j1 V=s  
6. （-j1 后面是线程数。第一次编译推荐用单线程）即可开始编译你要的固件了。

本套代码保证肯定可以编译成功。里面包括了 R20 所有源代码，包括 IPK 的。



二次编译：
-

```bash
cd lede
git pull
./scripts/feeds update -a && ./scripts/feeds install -a
make defconfig
make -j8 download
make -j$(($(nproc) + 1)) V=s
```

如果需要重新配置：
```bash
rm -rf ./tmp && rm -rf .config
make menuconfig
make -j$(($(nproc) + 1)) V=s
```

编译完成后输出路径：/lede/bin/targets

功能参照表
-
https://github.com/HTSMAIL/Openwrt20git-step/blob/master/%E5%8A%9F%E8%83%BD%E5%8F%82%E7%85%A7

广告过滤规则
-
https://github.com/HTSMAIL/Openwrt20git-step/blob/master/%E5%B9%BF%E5%91%8A%E8%BF%87%E6%BB%A4%E8%A7%84%E5%88%99

你可以自由使用，但源码编译二次发布请注明L大的 GitHub 仓库链接。谢谢合作！
=  
采用L大的源码，仓库地址
https://github.com/HTSMAIL/lede

上下键选择项目，左右键选择退出保存等。
输入 Y 选择该项目加入固件，N 不选泽，M 编译但不合入固件。
所有项目选完后保存再退出。保存时可以重命名，但只起保存当前配置的作用，编译有效的配置文件名还是 .config。
进入 menuconfig 第一眼感觉好复杂，不是专业的根本不知道都是啥，不过我们编译自己的固件不需要知道那么多，大多数默认设置就好了。

    Target System (x86) ---> #设置CPU类型（软路由所以选择x86,硬路由根据型号厂家选择自己的cpu)

    Subtarget (x86_64) ---> #CPU子选项

    Target Profile (Generic) ---> #厂家具体型号

    Target Images ---> #设置编译的格式（squashfs，ext4）

    Global build settings ---> #全局设置

    [ ] Advanced configuration options (for developers) ---- #高级配置选项

    [ ] Build the OpenWrt Image Builder #创建OpenWrt镜像生成器

    [ ] Build the OpenWrt SDK #创建OpenWrt SDK

    [ ] Package the OpenWrt-based Toolchain #打包基于OpenWrt的工具链

    [ ] Image configuration ---> #镜像配置

    Base system ---> #设置基础系统

    Administration ---> #管理

    Boot Loaders ---> #设置启动加载器

    Development --->

    Extra packages ---> #设置额外软件包

    Firmware ---> #设置固件

    Fonts --->　#设置字体

    Kernel modules ---> #设置一些接口模块，如LED，i2c，spi等

    Languages ---> #设置语言，如go，lua，node.js，php，Python等等

    Libraries ---> #设置库

    LuCI ---> #LuCi设置（这里重点开始选择- 3. Applications ->进去编译选择“y”，取消选“n”,说明在下边链接 ）

        1. collections luCI HTTPS支持 

        2. modules 模块，选中 Minify Lua Sources 压缩 Lua 脚本可增大固件中的可用空间

        3. applications 应用

        4. themes 主题

        5. protocols 支持协议

        6. libraries 支持docker json等库

        9. freifunk 社区产品

    Mail ---> mail 相关软件，协议等

    Multimedia ---> #设置多媒体，如FFmpeg

    Network ---> #网络配置，如bittorrent，firewall，download manager，VPN，ssh等等

    Sound ---> #声音配置

    Utilities ---> #设置实用程序

    Xorg ---> #字体配置

  拿 EA6500 v2 路由来做例子：

    Target System --> Broadcom BCM47xx/53xx(ARM)

    Target Profile --> Multiple devices

    Target Devices --> Linksys EA6500 V2

    Target Images --> squashfs


    LuCI --> 3. Applications --> 选择需要的插件，根据路由器的 flash 大小
    --> 4. Themes --> 默认就好，有的主题体积会比较大

