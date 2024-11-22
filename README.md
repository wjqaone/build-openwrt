
# 云编译OpenWrt

在线云编译，是github推出的一项服务，它提供了高性能的虚拟服务器环境，基于它可以进行构建、测试、打包、部署项目。利用它可以省去本地搭建或者购买服务器的时间成本，你只需要使用本仓库的代码，按照下方的使用方法，修改一些参数，即可开始编译openwrt，等待几个小时后，你就可以下载固件了。

说明：源码来自各位大佬分享，为了方便编译，做了一些修改，可以支持不同分支的opewrt源码，同时集成了打包img镜像的功能。

- 官方源码：    https://github.com/openwrt/openwrt      

- lede源码：    https://github.com/coolsnowwolf/lede  

- lienol源码：  https://github.com/Lienol/openwrt 

- immortalwrt源码： https://github.com/immortalwrt/immortalwrt

### 操作教程由“实用技能”提供 @shiyongjineng

#### 观看视频教程↓↓点击下方↓↓进行观看！

[![从零开始：自己编译OpenWrt系统！一个视频就够了！](https://res.cloudinary.com/marcomontalbano/image/upload/v1692411463/video_to_markdown/images/youtube--_3B-y73JRQ4-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/_3B-y73JRQ4 "从零开始：自己编译OpenWrt系统！一个视频就够了！")

[![openwrt在线编译教程](https://res.cloudinary.com/marcomontalbano/image/upload/v1692156705/video_to_markdown/images/youtube--6j4ofS0GT38-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=6j4ofS0GT38 "openwrt在线编译教程")

[![电视盒子专用：利用Flippy内核工具打包，将OpenWrt固件转成img镜像文件，](https://res.cloudinary.com/marcomontalbano/image/upload/v1692927730/video_to_markdown/images/youtube--EPNsHRj3eXE-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/EPNsHRj3eXE "电视盒子专用：利用Flippy内核工具打包，将OpenWrt固件转成img镜像文件，")


## 使用方法

1，注册账号

- 点击github.com 网站右上角的【Sign up】按钮，根据要求填写完成即可！

2，设置权限

- 右上角点击自己的头像，下拉菜单中选择【Settings/设置】 > 【Developer settings/开发者设置】 > 【Personal access tokens/个人访问令牌 > 【Tokens（classic）/令牌（经典）】 > 【 Generate new token/生成新令牌 】 ( Name: GITHUB_TOKEN, Select: public_repo )，其他选项根据自己需要可以多选，提交保存，复制系统生成的加密 KEY 的值，先保存到自己电脑的记事本，下一步会用到这个值。

- 打开仓库 https://github.com/xinlingduyu/build-openwrt ，点击右上的 Fork 按钮，复制一份仓库代码到自己的账户下，稍等几秒钟，提示 Fork 完成后，到自己的账户下访问自己仓库里的 build-openwrt 。在右上角的 Settings > Secrets > Actions > New repostiory secret ( Name: GH_TOKEN, Value: 填写刚才GITHUB_TOKEN的值 )，保存。并在左侧导航栏的 Actions > General > Workflow permissions 下选择 Read and write permissions 并保存。图示如下：



3，设置config
- 进入config文件夹，需要用哪个分支的源码，就打开哪个文件夹。
   
设置config文件，可以从本地设置好后，复制进去替换掉即可。


4，添加插件或主题

-  进入config文件夹，需要用哪个分支的源码，就打开哪个文件夹。打开diy-part2.sh文件，电视盒子必须安装amlogic插件，格式如下：

    #####Add a feed source
    
    echo 'src-git amlogic https://github.com/ophub/luci-app-amlogic' >>feeds.conf.default
    
   
5，开始编译，
 
 - 点击菜单栏的【Actions】，左边菜单栏选择编译流程（说明：通用编译适合常用设备，如果你是电视盒子，那么请选择电视盒子编译）
 
 
 7，下载固件
 
 
 由于时间仓促，修改可能不到位，后续慢慢补充！

8， 个人说明

步骤1: 注册与登录GitHub
访问 GitHub 并注册账号，如果已有账号则直接登录。
步骤2: 设置个人访问令牌
进入您的GitHub Settings -> Developer settings -> Personal Access Tokens。
点击“Generate new token”，命名为GITHUB_TOKEN，并勾选public_repo权限，创建后保存生成的Token。
步骤4: 配置密钥和权限
回到您的GitHub账号，在相应Fork后的build-openwrt仓库中找到Settings -> Secrets -> Actions，新增一个名为GH_TOKEN的秘密，将其值设置为您之前生成的Token。
确保在Workflow permissions下选择至少有Read and write permissions。
步骤5: 修改编译配置
进入fork后的仓库代码，浏览到config目录，根据您想要编译的OpenWrt源码分支选择相应的配置文件进行修改。对于特定设备，如电视盒子，还需按需编辑diy-part2.sh文件来添加必要的插件或源。
步骤6: 启动编译
返回GitHub仓库主页，点击Actions标签页，您会看到预定义的工作流。根据您的设备选择相应的编译流程开始执行。

进阶
配置ip，diy-part2.sh
```
# Modify default IP
sed -i 's/192.168.1.1/192.168.1.230/g' package/base-files/files/bin/config_generate
```
添加软件源，diy-part1.sh
```
# Add a feed source
# sed -i '$a src-git lienol https://github.com/Lienol/openwrt-package' feeds.conf.default
sed -i '$a src-git hwfuture https://github.com/hongweifuture/openwrt-packages' feeds.conf.default
sed -i '$a src-git pwdep https://github.com/hongweifuture/pwdep.git' feeds.conf.default
```

![image](https://github.com/user-attachments/assets/441d6d76-66b9-4ba6-bd4b-a0dc64803f56)

文件共提供多种类型供下载（根据编译时选择的Target Images配置），需要其他类型的请自行转换，下面是部分说明

![image](https://github.com/user-attachments/assets/7f6e9cdc-8bd4-4d30-9eff-6f929491ae07)

一般来说，用openwrt-x86-64-generic-squashfs-combined.img 或.gz 文件就可以了

包含squashfs字样是带overlay的，相当于windows的ghost，如果使用中发生配置错误，可直接恢复默认（也就是与手机的恢复出厂设置类似）。
squashfs就是设置,如果需要对固件进行比较彻底的出厂设置恢复，可直接在控制台下输入firstboot 然后输入yes ，再输入reboot -f 重启即可恢复到刷机时的配置。
应用说明
在线excel
在线excel说明插件详情

详情说明
选择LuCI 配置 添加插件应用：常用

LuCI —> Applications —> luci-app-accesscontrol #访问时间控制

LuCI —> Applications —> luci-app-adbyby-plus #广告屏蔽大师Plus +

LuCI —> Applications —> luci-app-arpbind #IP/MAC绑定

LuCI —> Applications —> luci-app-autoreboot #支持计划重启

LuCI —> Applications —> luci-app-ddns #动态域名 DNS（集成阿里DDNS客户端）

LuCI —> Applications —> luci-app-filetransfer #文件传输（可web安装ipk包）

LuCI —> Applications —> luci-app-firewall #添加防火墙

LuCI —> Applications —> luci-app-frpc #内网穿透 Frp

LuCI —> Applications —> luci-app-ipsec-virtuald #virtual服务器 IPSec

LuCI —> Applications —> luci-app-nlbwmon #网络带宽监视器

LuCI —> Applications —> luci-app-ramfree #释放内存

LuCI —> Applications —> luci-app-samba #网络共享（Samba）

LuCI —> Applications —> luci-app-sfe #Turbo ACC网络加速（集成FLOW,BBR,NAT,DNS…

LuCI —> Applications —> luci-app-违禁软件-plus #违禁软件打倒美帝Plus+

luci-app-违禁软件-plus —> Include 违禁软件 违禁软件 Plugin #SS 违禁软件插件

luci-app-违禁软件-plus —> Include 违禁软件 #违禁软件代理

luci-app-违禁软件-plus —> Include Trojan #Trojan代理

luci-app-违禁软件-plus —> Include 违禁软件2 #违禁软件2代理

luci-app-违禁软件-plus —> Include 违禁软件R Server #违禁软件服务器

LuCI —> Applications —> luci-app-unblockmusic #解锁网易云灰色歌曲3合1新版本

LuCI —> Applications —> luci-app-upnp #通用即插即用UPnP（端口自动转发）

LuCI —> Applications —> luci-app-vlmcsd #KMS服务器设置

LuCI —> Applications —> luci-app-vsftpd #FTP服务器

LuCI —> Applications —> luci-app-webadmin #Web管理页面设置

LuCI —> Applications —> luci-app-wifischedule #WiFi 计划

LuCI —> Applications —> luci-app-wirele违禁软件egdb #WiFi无线

LuCI —> Applications —> luci-app-wol #WOL网络唤醒

LuCI —> Applications —> luci-app-xlnetacc #迅雷快鸟

LuCI —> Applications —> luci-app-zerotier #ZeroTier内网穿透

以下是全部： 注：应用后面标记 “ * ” 为最近新添加

LuCI —> Applications —> luci-app-accesscontrol #访问时间控制

LuCI —> Applications —> luci-app-acme #ACME自动化证书管理环境（已弃）

LuCI —> Applications —> luci-app-adblock #ADB广告过滤

LuCI —> Applications —> luci-app-adbyby-plus #广告屏蔽大师Plus +

LuCI —> Applications —> luci-app-adbyby #广告过滤大师（已弃）

LuCI —> Applications —> luci-app-adkill #广告过滤（已弃）

LuCI —> Applications —> luci-app-advanced-reboot #Linksys高级重启

LuCI —> Applications —> luci-app-ahcp #支持AHCPd

LuCI —> Applications —> luci-app-airplay2 #Apple AirPlay2 无损音频接收服务器

LuCI —> Applications —> luci-app-aliddns #阿里DDNS客户端（已弃，集成至ddns）

LuCI —> Applications —> luci-app-amule #aMule下载工具

LuCI —> Applications —> luci-app-aria2 # Aria2下载工具

LuCI —> Applications —> luci-app-arpbind #IP/MAC绑定

LuCI —> Applications —> luci-app-asterisk #支持Asterisk电话服务器

LuCI —> Applications —> luci-app-attendedsysupgrade #固件更新升级相关

LuCI —> Applications —> luci-app-autoreboot #支持计划重启

LuCI —> Applications —> luci-app-baidupcs-web #百度网盘管理

LuCI —> Applications —> luci-app-bcp38 #BCP38网络入口过滤（不确定）

LuCI —> Applications —> luci-app-bird1-ipv4 #对Bird1-ipv4的支持

LuCI —> Applications —> luci-app-bird1-ipv6 #对Bird1-ipv6的支持

LuCI —> Applications —> luci-app-bird4 #Bird 4（未知）（已弃）

LuCI —> Applications —> luci-app-bird6 #Bird 6（未知）（已弃）

LuCI —> Applications —> luci-app-bmx6 #BMX6路由协议

LuCI —> Applications —> luci-app-bmx7 #BMX7路由协议（已弃）

LuCI —> Applications —> luci-app-caldav #联系人（已弃）

LuCI —> Applications —> luci-app-cifs-mount #CIFS/SMB挂载设置

LuCI —> Applications —> luci-app-cifsd #CIFS/SMB网络共享

LuCI —> Applications —> luci-app-cjdns #加密IPV6网络相关

LuCI —> Applications —> luci-app-clamav #ClamAV杀毒软件

LuCI —> Applications —> luci-app-commands #Shell命令模块

LuCI —> Applications —> luci-app-cshark #CloudShark捕获工具

LuCI —> Applications —> luci-app-ddns #动态域名 DNS（集成阿里DDNS客户端）

LuCI —> Applications —> luci-app-diag-core #core诊断工具

LuCI —> Applications —> luci-app-diskman #磁盘管理工具

luci-app-diskman —> Include btrfs-progs #新型的写时复制 (COW)

luci-app-diskman —> Include lsblk #lsblk命令 用于列出所有可用块设备的信息

luci-app-diskman —> Include mdadm #mdadm命令 用于创建、管理、监控RAID设备的工具

luci-app-diskman —> Include kmod-md-raid456 #RAID 4,5,6 驱动程序模块（已弃）

luci-app-diskman —> Include kmod-md-linear #RAID 驱动程序模块（已弃）

LuCI —> Applications —> luci-app-dnscrypt-proxy #DNSCrypt解决DNS污染

LuCI —> Applications —> luci-app-dnsforwarder #DNSForwarder防DNS污染

LuCI —> Applications —> luci-app-dnspod #DNSPod动态域名解析（已弃）

LuCI —> Applications —> luci-app-dockerman #Docker容器

LuCI —> Applications —> luci-app-dump1090 #民航无线频率（不确定）

LuCI —> Applications —> luci-app-dynapoint #DynaPoint（未知）

LuCI —> Applications —> luci-app-e2guardian #Web内容过滤器

LuCI —> Applications —> luci-app-familycloud #家庭云盘

LuCI —> Applications —> luci-app-filetransfer #文件传输（可web安装ipk包）

LuCI —> Applications —> luci-app-firewall #添加防火墙

LuCI —> Applications —> luci-app-flowoffload #Turbo ACC网络加速（集成FLOW,BBR,NAT,DNS…

LuCI —> Applications —> luci-app-freifunk-diagnostics #freifunk组件 诊断（未知）

LuCI —> Applications —> luci-app-freifunk-policyrouting #freifunk组件 策略路由（未知）

LuCI —> Applications —> luci-app-freifunk-widgets #freifunk组件 索引（未知）

LuCI —> Applications —> luci-app-frpc #内网穿透Frp客户端

LuCI —> Applications —> luci-app-frps #内网穿透Frp服务端

LuCI —> Applications —> luci-app-fwknopd #Firewall Knock Operator服务器

LuCI —> Applications —> luci-app-guest-wifi #WiFi访客网络

LuCI —> Applications —> luci-app-gfwlist #GFW域名列表（已弃）

LuCI —> Applications —> luci-app-haproxy-tcp #HAProxy负载均衡-TCP

LuCI —> Applications —> luci-app-hd-idle #硬盘休眠

LuCI —> Applications —> luci-app-hnet #Homenet Status家庭网络控制协议

LuCI —> Applications —> luci-app-https-dns-proxy #通过HTTPS代理为DNS提供Web UI *

LuCI —> Applications —> luci-app-ipsec-virtuald #virtual服务器 IPSec

LuCI —> Applications —> luci-app-kodexplorer #KOD可道云私人网盘

LuCI —> Applications —> luci-app-kooldns #virtual服务器 ddns替代方案（已弃）

LuCI —> Applications —> luci-app-koolproxy #KP去广告（已弃）

LuCI —> Applications —> luci-app-lxc #LXC容器管理

LuCI —> Applications —> luci-app-meshwizard #网络设置向导

LuCI —> Applications —> luci-app-minidlna #完全兼容DLNA / UPnP-AV客户端的服务器软件

LuCI —> Applications —> luci-app-mjpg-streamer #兼容Linux-UVC的摄像头程序

LuCI —> Applications —> luci-app-mtwifi #MTWiFi驱动的支持 （已弃）

LuCI —> Applications —> luci-app-mmc-over-gpio #添加SD卡操作界面（已弃）

LuCI —> Applications —> luci-app-multiwan #多拨虚拟网卡（已弃，移至syncdial）

LuCI —> Applications —> luci-app-mwan #MWAN负载均衡（已弃）

LuCI —> Applications —> luci-app-music-remote-center #PCHiFi 数字转盘遥控

LuCI —> Applications —> luci-app-mwan3 #MWAN3负载均衡

LuCI —> Applications —> luci-app-mwan3helper #MWAN3分流助手

LuCI —> Applications —> luci-app-n2n_v2 #N2N内网穿透 N2N v2 virtual服务

LuCI —> Applications —> luci-app-netdata #Netdata实时监控（图表）

LuCI —> Applications —> luci-app-nfs #NFS网络共享

LuCI —> Applications —> luci-app-nft-qos #QOS流控 Nftables版

LuCI —> Applications —> luci-app-ngrokc #Ngrok 内网穿透（已弃）

LuCI —> Applications —> luci-app-nlbwmon #网络带宽监视器

LuCI —> Applications —> luci-app-noddos #NodDOS Clients 阻止DDoS攻击

LuCI —> Applications —> luci-app-nps #内网穿透nps

LuCI —> Applications —> luci-app-ntpc #NTP时间同步服务器

LuCI —> Applications —> luci-app-ocserv #OpenConnect virtual服务

LuCI —> Applications —> luci-app-olsr #OLSR配置和状态模块

LuCI —> Applications —> luci-app-olsr-services #OLSR服务器

LuCI —> Applications —> luci-app-olsr-viz #OLSR可视化

LuCI —> Applications —> luci-app-ocserv #OpenConnect virtual服务（已弃）

LuCI —> Applications —> luci-app-openvirtual** #Openvirtual客户端

LuCI —> Applications —> luci-app-openvirtual-server #易于使用的Openvirtual服务器 Web-UI

LuCI —> Applications —> luci-app-oscam #OSCAM服务器（已弃）

LuCI —> Applications —> luci-app-p910nd #打印服务器模块

LuCI —> Applications —> luci-app-pagekitec #Pagekite内网穿透客户端

LuCI —> Applications —> luci-app-polipo #Polipo代理(是一个小型且快速的网页缓存代理)

LuCI —> Applications —> luci-app-pppoe-relay #PPPoE NAT穿透 点对点协议（PPP）

LuCI —> Applications —> luci-app-p p t p-server #virtual服务器 p p t p（已弃）

LuCI —> Applications —> luci-app-privoxy #Privoxy网络代理(带过滤无缓存)

LuCI —> Applications —> luci-app-ps3netsrv #PS3 NET服务器（用于加载蓝光/游戏ISO/PKG）

LuCI —> Applications —> luci-app-qbittorrent #BT下载工具（qBittorrent）

LuCI —> Applications —> luci-app-qos #流量服务质量(QoS)流控

LuCI —> Applications —> luci-app-radicale #CalDAV/CardDAV同步工具

LuCI —> Applications —> luci-app-ramfree #释放内存

LuCI —> Applications —> luci-app-rclone #命令行云端同步工具

Include rclone-webui #Rclone界面

Include rclone-ng (another webui) #Rclone另一个界面

Include fuse-utils (mount cloud storage) #fuse-utils（挂载云存储）

LuCI —> Applications —> luci-app-rp-pppoe-server #Roaring Penguin PPPoE Server 服务器

LuCI —> Applications —> luci-app-samba #网络共享（Samba）

LuCI —> Applications —> luci-app-samba4 #网络共享（Samba4）

LuCI —> Applications —> luci-app-sfe #Turbo ACC网络加速（flowoffload二选一）

LuCI —> Applications —> luci-app-违禁软件 #SS打倒美帝（已弃）

LuCI —> Applications —> luci-app-违禁软件-libes #SS-libev服务端

LuCI —> Applications —> luci-app-shairplay #支持AirPlay功能

LuCI —> Applications —> luci-app-siitwizard #SIIT配置向导 SIIT-Wizzard

LuCI —> Applications —> luci-app-simple-adblock #简单的广告拦截

LuCI —> Applications —> luci-app-smartdns #SmartDNS本地服务器（已弃）

LuCI —> Applications —> luci-app-softethervirtual** #SoftEther virtual服务器 NAT穿透

LuCI —> Applications —> luci-app-splash #Client-Splash是无线MESH网络的一个热点认证系统

LuCI —> Applications —> luci-app-sqm #流量智能队列管理（QOS）

LuCI —> Applications —> luci-app-squid #Squid代理服务器

LuCI —> Applications —> luci-app-违禁软件-plus #违禁软件打倒美帝Plus+

luci-app-违禁软件-plus —> Include 违禁软件 New Version #新SS代理（已弃）

luci-app-违禁软件-plus —> Include 违禁软件 Simple-obfs Plugin #simple-obfs简单混淆工具（已弃）

luci-app-违禁软件-plus —> Include 违禁软件 违禁软件 Plugin #SS 违禁软件插件

luci-app-违禁软件-plus —> Include 违禁软件 #违禁软件代理

luci-app-违禁软件-plus —> Include Trojan #Trojan代理

luci-app-违禁软件-plus —> Include NaiveProxy #NaiveProxy代理 *

luci-app-违禁软件-plus —> Include 违禁软件2 #违禁软件2代理

luci-app-违禁软件-plus —> Include Kcptun #Kcptun加速

luci-app-违禁软件-plus —> Include 违禁软件R Server #违禁软件服务器

luci-app-违禁软件-plus —> Include DNS2SOCKS #DNS服务器（已弃）

luci-app-违禁软件-plus —> Include 违禁软件R Socks and Tunnel（已弃）

luci-app-违禁软件-plus —> Include Socks Server #socks代理服务器（已弃）

LuCI —> Applications —> luci-app-违禁软件-pro #违禁软件-Pro（已弃）

LuCI —> Applications —> luci-app-违禁软件server-python #违禁软件R Python服务器

LuCI —> Applications —> luci-app-statistics #流量监控工具

LuCI —> Applications —> luci-app-syncdial #多拨虚拟网卡（原macvlan）

LuCI —> Applications —> luci-app-tinyproxy #Tinyproxy是 HTTP(S)代理服务器

LuCI —> Applications —> luci-app-transmission #BT下载工具

LuCI —> Applications —> luci-app-travelmate #旅行路由器

LuCI —> Applications —> luci-app-ttyd #网页终端命令行

LuCI —> Applications —> luci-app-udpxy #udpxy做组播服务器

LuCI —> Applications —> luci-app-uhttpd #uHTTPd Web服务器

LuCI —> Applications —> luci-app-unblockmusic #解锁网易云灰色歌曲3合1新版本

UnblockNeteaseMusic Golang Version #Golang版本

UnblockNeteaseMusic NodeJS Version #NodeJS版本

LuCI —> Applications —> luci-app-unblockneteasemusic-go #解除网易云音乐（合并）

LuCI —> Applications —> luci-app-unblockneteasemusic-mini #解除网易云音乐（合并）

LuCI —> Applications —> luci-app-unbound #Unbound DNS解析器

LuCI —> Applications —> luci-app-upnp #通用即插即用UPnP（端口自动转发）

LuCI —> Applications —> luci-app-usb-printer #USB 打印服务器

LuCI —> Applications —> luci-app-违禁软件-server #违禁软件 服务器

LuCI —> Applications —> luci-app-违禁软件-pro #违禁软件透明代理（已弃，集成违禁软件）

LuCI —> Applications —> luci-app-verysync #微力同步

LuCI —> Applications —> luci-app-vlmcsd #KMS服务器设置

LuCI —> Applications —> luci-app-vnstat #vnStat网络监控（图表）

LuCI —> Applications —> luci-app-virtualbypass #virtual** BypassWebUI 绕过virtual设置

LuCI —> Applications —> luci-app-vsftpd #FTP服务器

LuCI —> Applications —> luci-app-watchcat #断网检测功能与定时重启

LuCI —> Applications —> luci-app-webadmin #Web管理页面设置

LuCI —> Applications —> luci-app-webshell #网页命令行终端（已弃）

LuCI —> Applications —> luci-app-wifischedule #WiFi 计划

LuCI —> Applications —> luci-app-wireguard #virtual服务器 WireGuard状态

LuCI —> Applications —> luci-app-wirele违禁软件egdb #WiFi无线

LuCI —> Applications —> luci-app-wol #WOL网络唤醒

LuCI —> Applications —> luci-app-wrtbwmon #实时流量监测

LuCI —> Applications —> luci-app-xlnetacc #迅雷快鸟

LuCI —> Applications —> luci-app-zerotier #ZeroTier内网穿透

支持 iPv6：
1、Extra packages —> ipv6helper （选定这个后下面几项自动选择了）

Network —> odhcp6c

Network —> odhcpd-ipv6only

LuCI —> Protocols —> luci-proto-ipv6

LuCI —> Protocols —> luci-proto-ppp

2、打开适用于VMware的VM Tools

Utilities —> open-vm-tools #打开适用于VMware的VM Tools

Utilities —> open-vm-tools-fuse #打开适用于VMware的VM Tools

3、第二次编译：

cd lede # 进入LEDE目录

git pull # 同步更新大雕源码

./scripts/feeds update -a && ./scripts/feeds install -a # 更新Feeds

rm -rf ./tmp && rm -rf .config # 清除编译配置和缓存

make menuconfig # 进入编译配置菜单

make -jn V=99 # 开始编译 n=线程数+1，例如4线程的I5填-j5

表格

序号	名称	说明
（1）	openwrt-x86-64-generic-squashfs-combined.img 或.gz	带引导分区文件，也就是刷完后可以直接启动无需做设置，推荐使用！
（2）	openwrt-x86-64-generic-squashfs-combined.vmdk	带引导分区的虚拟机Vmware文件，VM WorkStation直接选择磁盘后可直接启动无需再单独设置（注意：非ESXI文件，ESXI建议使用(1)转换后使用）。
（3）	openwrt-x86-64-rootfs-squashfs.img或.gz	分区文件，刷此文件，只是把系统刷到了分区（分区格式需为Ext4），需要单独设置grub或者syslinux来进行引导。
（4）	openwrt-x86-64-generic-squashfs-combined-efi.img或.gz	带UEFI固件为支持efi启动，原理同（1）的说明。
（5）	openwrt-x86-64-generic-ext4-combined.img 或.gz	为Ext4分区文件，可作为升级使用直接写入到分区即可。efi.img同理
（6）	openwrt-x86-64-combined-squashfs.iso	系统镜像文件，可以使用ultraiso或类似工具直接写入到磁盘即可，efi 文件同理。
