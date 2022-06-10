1.下载脚本

$ wget https://github.com/ycgkwyc/openvpn-install.git

2.执行安装脚本
$ bash openvpn-install.sh

3.安装过程中会有一些交互输入：

First, provide the IPv4 address of the network interface you want OpenVPN
listening to.
IP address: 12.34.56.78

按回车确定，选择当前 WAN IP。

Which protocol do you want for OpenVPN connections?
1) UDP (recommended)
2) TCP
默认选择 UDP。

What port do you want OpenVPN listening to?
Port: 1194
使用默认 1194 端口.

Which DNS do you want to use with the VPN?
1) Current system resolvers
2) 1.1.1.1
3) Google
4) OpenDNS
5) Verisign
DNS [1-5]: 1
选择1，使用系统默认的 DNS 解析配置。

Finally, tell me your name for the client certificate.
Please, use one word only, no special characters.
Client name: client
client 证书的名字，默认为 client。如果只是生成一个客户端用户文件名，保留默认值即可。

配置已经完成。按照屏幕提示按任意键开始生成即可。

Okay, that was all I needed. We are ready to set up your OpenVPN server now.
Press any key to continue...
确认服务运行状态。正常情况下，OpenVPN 服务就已经开始在后台运行了。可以通过查看进程确认：

root@ubuntu:~# ps -ef | grep vpn
nobody   14173     1  0 06:30 ?        00:00:00 /usr/sbin/openvpn --daemon ovpn-server --status /run/openvpn/server.status 10 --cd /etc/openvpn --script-security 2 --config /etc/openvpn/server.conf --writepid /run/openvpn/server.pid
大功告成，分发客户端配置文件。将配置文件拷到客户端。

$ scp <机器名>:/root/client.ovpn .
使用 openvpn 客户端读取配置文件，并连接即可。

日常维护

要停止 openvpn 服务：

$ systemctl stop openvpn@server
启动 openvpn 服务：

$ systemctl start openvpn@server
至此，OpenVPN 的快速安装就完成了。
