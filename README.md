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

`sudo apt-get update` 

然后安装依赖输入

`
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf
`

3. 使用 `git clone https://github.com/coolsnowwolf/lede` 命令下载好源代码，然后 `cd lede` 进入目录

        vi feeds.conf.default
推荐下面的软件包，几乎涵盖了你需要插件

        src-git kenzo https://github.com/V2RaySSR/openwrt-packages
        src-git small https://github.com/V2RaySSR/small

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

5. `make -j8 download V=s` 下载dl库（国内请尽量全局科学上网）


6. 输入 `make -j1 V=s` （-j1 后面是线程数。第一次编译推荐用单线程）即可开始编译你要的固件了。

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

你可以自由使用，但源码编译二次发布请注明L大的 GitHub 仓库链接。谢谢合作！
=  
采用L大的源码，仓库地址
https://github.com/HTSMAIL/lede
