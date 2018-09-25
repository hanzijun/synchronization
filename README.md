# synchronization
(1) 服务器端配置 
安装ntp:$ sudo apt install ntp

编辑配置文件/etc/ntp.conf
$ sudo vim /etc/ntp.conf

添加如下内容：
server 127.127.1.0 # local clock
fudge 127.127.1.0 stratum 10
为了让本机的硬件时间和本机的ntp服务进行时间同步。

重启ntp服务：$ sudo /etc/init.d/ntp restart

---------------------
(2) 客户端配置 
安装ntp：$ sudo apt install ntp

编辑配置文件/etc/ntp.conf
$ sudo vim /etc/ntp.conf

添加如下内容：
server 192.168.2.4  # 笔记本的ip地址

重启ntp服务：$ sudo /etc/init.d/ntp restart

$ sudo /usr/sbin/ntpdate server.IP

---------------------
为了避免每次时间同步都要输入上述指令
可以在/etc/crontab文件中配置，每分钟进行一次时间同步。

$ sudo vim /etc/crontab

末尾添加如下内容：

* * * * * /usr/sbin/ntpdate 192.168.2.4;/sbin/hwlocal -w

---------------------
(3) 验证时间误差
安装clockdiff： sudo apt-get install iputils-clockdiff
$ sudo clockdiff server.IP
