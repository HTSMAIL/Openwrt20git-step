	Openwrt修改默认IP,主机名，密码
	opnwrt固件源码修改登陆密码
	默认情况下root是没有密码的，需设定密码才能开启ssh

	修改shadow文件，位于package/base-files/files/etc/shadow

	添加root默认密码为admin,密文：$1$wEehtjxj$YBu4quNfVUjzfv8p/PBo5. 将此密文添加到上图中root:和：中间即可。效果就像下面这样

	root:$1$wEehtjxj$YBu4quNfVUjzfv8p/PBo5.:0:0:99999:7:::

	密码经过加密，将密码修改成admin

	密码文件在 etc目录里，编译后的依旧在etc目录里

	默认的shadow文件内的内容如下

	root::0:0:99999:7:::

	daemon:*:0:0:99999:7:::

	ftp:*:0:0:99999:7:::

	network:*:0:0:99999:7:::

	nobody:*:0:0:99999:7:::

	设置默认中文，修改主机名，添加并修改默认主题，设定时区
	默认中文，添加并默认主题

	修改feeds/luci/libs/web/root/etc/config

	option lang auto改为option lang zh_cn

	并添加

	config internal languages

	option en 'English' 

	option zh_cn 'chinese'

	opnwrt固件源码修改主机名
	/package/base-files/files/bin下的config_generate中修改     hostname

        set system.@system[-1].hostname='QingLink'

        set system.@system[-1].timezone='CST-8'

        set system.@system[-1].ttylogin='0'

        set system.@system[-1].log_size='64'

        set system.@system[-1].urandom_seed='0'

 

        delete system.ntp

        set system.ntp='timeserver'

        set system.ntp.enabled='1'

        set system.ntp.enable_server='1'

        add_list system.ntp.server='0.cn.pool.ntp.org'

        add_list system.ntp.server='1.pool.ntp.org'

        add_list system.ntp.server='2.cn.pool.ntp.org'

        add_list system.ntp.server='3.cn.ntp.org.cn'

	option hostname Openwrt 设定主机名
	option timezone Asia/Shanghai 时区设置为亚洲/上海

	option timezone CST-8 正8区

list server 就是ntp服务器了。

	opnwrt固件源码“无线名称SSID”修改
	固件源码“无线名称SSID”的修改的文件同样也在package目录中

/package/kernel/mac80211/files/lib/wifi目录下的mac80211.sh文件中

	这是我修改的，WiFi名称为mac地址后6位

set wireless.default_radio${devidx}.ssid=OpenWrt_$(cat /sys/class/ieee80211/${dev}/macaddress|awk -F ":" '{print $4""$5""$6 }'| tr a-z A-Z)

		直接修改对应的dts文件，在openwrt/target/linux/ramips/dts目录下，对应在make menuconfig里面选的什么型号，找到对应的DTS，需改里面model = "........";这后面的，就可以了

		opnwrt固件源码修改默认IP也很简单
		package/base-files/files/bin/config_generate文件文本方式打开

		搜索192.168.1.1就找到位置了，时区也在该文件里 不会就用正常使用的路由配置文件对比修改(照葫芦画瓢)就好了


		openwrt默认主题为luci-theme-bootstrap，可在web界面进行修改，也可直接在代码中修改配置信息，默认自己的主题

		修改前：openwrt默认luci主题luci-theme-bootstrap

 .config - OpenWrt Configuration
 > LuCI > 4. Themes ──────────────────────────────────────────────────────────────────────────────
  ┌──────────────────────────────────────── 4. Themes ─────────────────────────────────────────┐
  │  Arrow keys navigate the menu.  <Enter> selects submenus ---> (or empty submenus ----).    │  
  │  Highlighted letters are hotkeys.  Pressing <Y> includes, <N> excludes, <M> modularizes    │  
  │  features.  Press <Esc><Esc> to exit, <?> for Help, </> for Search.  Legend: [*] built-in  │  
  │  [ ] excluded  <M> module  < > module capable                                              │  
  │ ┌────────────────────────────────────────────────────────────────────────────────────────┐ │  
  │ │         <*> luci-theme-argon............................................. Argon Theme  │ │  
  │ │         -*- luci-theme-bootstrap........................... Bootstrap Theme (default)  │ │  
  │ │         < > luci-theme-material....................................... Material Theme  │ │  
  │ │         < > luci-theme-openwrt................................ LuCI OpenWrt.org theme  │ │  
  │ │                                                                                        │ │  
  │ │                                                                                        │ │  
  │ │                                                                                        │ │  
  │ └────────────────────────────────────────────────────────────────────────────────────────┘ │  
  ├────────────────────────────────────────────────────────────────────────────────────────────┤  
  │                  <Select>    < Exit >    < Help >    < Save >    < Load >                  │  
  └────────────────────────────────────────────────────────────────────────────────────────────┘  
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
 
 
 
 	> LuCI > 4. Themes ─────────────────────────────────────────────────────────────────────────
  ┌────────────────────────────────────── 4. Themes ──────────────────────────────────────┐
  │  Arrow keys navigate the menu.  <Enter> selects submenus ---> (or empty submenus      │  
  │  ----).  Highlighted letters are hotkeys.  Pressing <Y> includes, <N> excludes, <M>   │  
  │  modularizes features.  Press <Esc><Esc> to exit, <?> for Help, </> for Search.       │  
  │  Legend: [*] built-in  [ ] excluded  <M> module  < > module capable                   │  
  │ ┌───────────────────────────────────────────────────────────────────────────────────┐ │  
  │ │      -*- luci-theme-argon............................................. Argon Theme│ │  
  │ │      <*> luci-theme-bootstrap........................... Bootstrap Theme (default)│ │  
  │ │      < > luci-theme-material....................................... Material Theme│ │  
  │ │      < > luci-theme-openwrt................................ LuCI OpenWrt.org theme│ │  
  │ │                                                                                   │ │  
  │ │                                                                                   │ │  
  │ │                                                                                   │ │  
  │ └───────────────────────────────────────────────────────────────────────────────────┘ │  
  ├───────────────────────────────────────────────────────────────────────────────────────┤  
  │               <Select>    < Exit >    < Help >    < Save >    < Load >                │  
  └───────────────────────────────────────────────────────────────────────────────────────┘  

仅此记录

		
		进入路径openwrt/feeds/luci/collections/luci，修改Makefile（适用于openwrt版本19.07,不同的版本，会稍微不同）

		将LUCI_DESCRIPTION中，bootstrap 替换为 argon
		将LUCI_DEPENDS中，+luci-theme-bootstrap 替换为 +luci-theme-argon

		include $(TOPDIR)/rules.mk

		LUCI_TYPE:=col
		LUCI_BASENAME:=luci

		LUCI_TITLE:=LuCI interface with Uhttpd as Webserver (default)
		LUCI_DESCRIPTION:=Standard OpenWrt set including full admin with ppp support and the default argon theme
		LUCI_DEPENDS:= \
			+uhttpd +luci-mod-admin-full +luci-theme-argon \
			+luci-app-firewall +luci-app-opkg +luci-proto-ppp +libiwinfo-lua +IPV6:luci-proto-ipv6 \
			+rpcd-mod-rrdns

	PKG_LICENSE:=Apache-2.0

include ../../luci.mk

# call BuildPackage - OpenWrt buildroot signature
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
			保存，重新进入menuconfig

			此时默认luci主题已经更改为luci-theme-argon

			 .config - OpenWrt Configuration
 
