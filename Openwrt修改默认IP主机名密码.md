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
