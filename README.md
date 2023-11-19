# Openwrt20git-step编译步骤究极说明

#  关于虚拟机如何运行 
出处：https://blog.csdn.net/ballack_linux/article/details/81331527

    简述： 由于.img文件没法被vmware直接使用，需要转换成vmdk格式的，那么需要使用qemu-img工具。

    #ubuntu下直接使用 ：    
    sudo  apt-get  install  qemu-utils  -y
    #输入指令
    sudo qemu-img convert -f raw openwrt-xxx.img -O vmdk openwrt-xxx.vmdk

#改网口地址（默认网关ip）

        ```bash
        vim /etc/config/network
        ```
火力全开

     #一键起飞编译方法
    make V=99 -j 96  
    #主题单独编译
    make package/luci-theme-argon_new/compile V=99
# 以lede为例自定义一个自己的专属wrt固件
采用L大的源码，仓库地址
https://github.com/HTSMAIL/lede

# 编译好的固件：点击链接加入群聊【编译-软/硬路由-储存站】：
https://jq.qq.com/?_wv=1027&k=kvcPp7K8

#教程内容：
中文：如何编译自己需要的 OpenWrt 固件
-
注意：
-
1. **不**要用 **root** 用户 git 和编译！！！
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.1.1, 密码 password

注意
不要用 root 用户进行编译
国内用户编译前最好准备好梯子
默认登陆IP 192.168.1.1 密码 password
编译命令
首先装好 Linux 系统，推荐 Debian 11 或 Ubuntu LTS

安装编译依赖
```bash
sudo apt update -y
sudo apt full-upgrade -y
sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libglib2.0-dev libgmp3-dev libltdl-dev \
libmpc-dev libmpfr-dev libncurses5-dev libncursesw5-dev libreadline-dev libssl-dev libtool lrzsz \
mkisofs msmtp nano ninja-build p7zip p7zip-full patch pkgconf python2.7 python3 python3-pyelftools \
libpython3-dev qemu-utils rsync scons squashfs-tools subversion swig texinfo uglifyjs upx-ucl unzip \
vim wget xmlto xxd zlib1g-dev python3-setuptools
```
下载源代码，更新 feeds 并选择配置
```bash
git clone https://github.com/coolsnowwolf/lede
cd lede
```
```bash
./scripts/feeds update -a && ./scripts/feeds install -a
```
```bash
make menuconfig
```
下载 dl 库，编译固件 （-j 后面是线程数，第一次编译推荐用单线程）
```bash
make download -j8
```
```bash
make V=s -j1
```
本套代码保证肯定可以编译成功。里面包括了 R23 所有源代码，包括 IPK 的。

你可以自由使用，但源码编译二次发布请注明我的 GitHub 仓库链接。谢谢合作！

二次编译：
```bash
cd lede
git pull
./scripts/feeds update -a && ./scripts/feeds install -a
make defconfig
make download -j8
```
```bash
make V=s -j$(nproc)
```
如果需要重新配置：
```bash
rm -rf ./tmp && rm -rf .config
make menuconfig
make V=s -j$(nproc)
```
编译完成后输出路径：bin/targets

如果你使用 WSL/WSL2 进行编译
由于 WSL 的 PATH 中包含带有空格的 Windows 路径，有可能会导致编译失败，请在 make 前面加上：

PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
由于默认情况下，装载到 WSL 发行版的 NTFS 格式的驱动器将不区分大小写，因此大概率在 WSL/WSL2 的编译检查中会返回以下错误：

Build dependency: OpenWrt can only be built on a case-sensitive filesystem 
一个比较简洁的解决方法是，在 git clone 前先创建 Repository 目录，并为其启用大小写敏感：

# 以管理员身份打开终端
```PS > fsutil.exe file setCaseSensitiveInfo <your_local_lede_path> enable```
# 将本项目 git clone 到开启了大小写敏感的目录 <your_local_lede_path> 中
```PS > git clone git@github.com:coolsnowwolf/lede.git <your_local_lede_path>```
对已经 git clone 完成的项目目录执行 fsutil.exe 命令无法生效，大小写敏感只对新增的文件变更有效。


修改源
推荐下面的软件包，几乎涵盖了你需要插件
```vi feeds.conf.default```
```bash


src-git kenzo https://github.com/kenzok8/openwrt-packages
src-git small https://github.com/kenzok8/small


src-git https://github.com/kenzok8/small-package
    ```


        
        备用地址
```bash
       src-git https://github.com/HTSMAIL/openwrt-packages
       src-git https://github.com/HTSMAIL/small
```
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
```bash
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
```
  拿 EA6500 v2 路由来做例子：
```bash
    Target System --> Broadcom BCM47xx/53xx(ARM)

    Target Profile --> Multiple devices

    Target Devices --> Linksys EA6500 V2

    Target Images --> squashfs


    LuCI --> 3. Applications --> 选择需要的插件，根据路由器的 flash 大小
    --> 4. Themes --> 默认就好，有的主题体积会比较大
```
