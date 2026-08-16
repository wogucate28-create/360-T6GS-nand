# 360-T6GS-nand
仅整合
360 T6GS nand 电信定制版刷机教程及工具整合
原创作者为恩山论坛@午时三刻
刷机教程：
1：先将路由器重置，然后进入路由器后台升级界面，将T6GS-4.1.0.2669-rel-upgrade.bin(感谢@fourkox大佬提供)刷进去降级，刷完后再重置一次。
2：给路由器拆机，拆机时注意路由器底部标签隐藏了一颗螺丝，拆开后把杜邦线焊接在路由器背面右上角的GND、RX、TX触点上，然后把三根杜邦线跟USB转TTL模块连接，GND对GND，RX对TX，TX对RX。
3：接好TTL后，给路由器通电，再把USB转TTL模块连接电脑，并打开putty软件，填写好CDM串口(电脑设备管理器那里可以看到串口是多少)，波特率115200，直接跑码，看到Press the [f] key and hit [enter] to enter failsafe mode Press the [1], [2], [3] or [4] key and hit [enter] to select the debug level后按f键回车就能进入failsafe模式了。
4：进入failsafe模式后直接输入下面两行命令开启telnet：
mount_root
sed -i 's/.*local debug=.*/\tlocal debug=1/' /etc/init.d/telnet
再输入下面命令修改root密码：
passwd root
5：拔出USB转TTL模块，路由器网线连接电脑并重新通电让路由系统正常启动，打开hfs软件，把u-boot-T6GS.bin文件直接鼠标拉到hfs左边空白界面，点一下上面u-boot-T6GS.bin，你会看到一行http://192.168.2.x:8080/u-boot-T6GS.bin链接，复制链接。打开putty，选telnet，填上路由器地址回车，看到Openwrt login：后填上root回车，再填上之前修改的root密码回车进入BusyBox界面。
6：进入BusyBox界面后，输入cd /tmp切换到tmp目录，再输入wget http://192.168.2.x:8080/u-boot-T6GS.bin(那个x换成你的实际数字)把u-boot-T6GS.bin文件传输到tmp目录。
7：输入mtd write u-boot-T6GS.bin u-boot命令刷入u-boot，显示Writing from u-boot-T6GS.bin to u-boot ...就是刷入成功
8：断电状态下按住复位键再通电，看到绿灯闪三到四下松手，在浏览器网址栏输入192.168.1.1进入UBOOT界面，按页面提示刷入固件即可。
