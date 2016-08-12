Unix and Linux System Administrator Handbook
============================================================

脚本
------------------------------

变量名与 ＝ 之间不能有空格，防止与命令冲突

环境变量自动加入到 bash 变量名字空间。使用 export 将变量放入环境变量中。

过滤命令
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

cut -d char -f field

sort -b -f -k -n -r -t -u

tee /dev/tty

bash
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

$# 命令参数个数
$* 所有命令

test
page 44

网络
------------------------------

IP internet protocol rfc791
ICMP internet control message protocol  rfc792
ARP address resolution protocol rfc826
UDP user datagram protocol rfc768
TCP transmission control protocol rfc793

Application layer
Transport layer
network layer
link layer
physical layer

packet: header and payload
header: from, to, checksum, protocol-specific information,

link layer: frame
ip layer: packet
tcp layer: segment

ip layer 将 packet 分成 mtu

地址协议：
* MAC (media access control)
* IPv4, IPv6
* hostname

ip address 是区分 net interfaces，而不是 machine

128.138.243.0/26

内网地址：
10.0.0.0
172.16.0.0
192.168.0.0

Routing table ::

    netstat -rn

当接入设备到网络，设备通常会获取 IP 地址，设置默认 route, 设置 DNS 服务器。

dhcp 分配项
* ip address, netmask
* gateways 默认 route
* dns
* syslog host
* wins ， ntp, proxy,
* tftp

dgcp client 首先发送广播消息。如果 dhcp server 收到消息，同客户端协商分配 ip 地址。

Email
------------------------------

组成：

* mail user agent MUA 用户读写邮件
* mail submission agent MSA
* mail transport agent MTA
* delivery agent DA
* access agent AA

MTA 工作：

* 接收远程邮件服务器 email 消息
* 解析地址
* 重写地址
* 转发

mail 消息分成三个部分：

* envelop
* headers
* body

envelop 决定消息发送到哪

postfix page 830

mydestination
virtual_alias_domains
virtual_mailbox_domains

安全
------------------------------

查看服务器运行的服务 ::

    $ netstat -an | grep LISTEN

查看端口对应程序 ::

    $ sudo fuser 22/tcp
    $ sudo lsof -i:22
