https://www.youtube.com/watch?v=XKfhOQWrUVw

deny everything by default policy

accept everything by default policy

filtering:
1. source address spoofing


iptables --flush

-A append -I insert 
-i interface
-j
-p protocol
-s source 
-d destination
--dport destination port
-m match

iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT
iptables --policy INPUT DROP
iptables --policy OUTPUT DROP
iptables --policy FORWARD DROP

allow ssh:
SERVER_IP=192.168.0.3
NETWORK="192.168.0.0/24"
iptables -I INPUT -i eth0 -p tcp -s $NETWORK -d $SERVER_IP --dport 22 -j ACCEPT

allow icmp ping:
iptables -I INPUT -i eth0 -p icmp --icmp-type 8 -s 0/0 -d $SERVER_IP -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
iptables -I OUTPUT -i eth0 -p icmp --icmp-type 0 -s $SERVER_IP -d 0/0 -m state --state ESTABLISHED,RELATED -j ACCEPT

targets:
ACCEPT
DROP
REJECT
RETURN

standalone firewall:

SERVER_IP=192.168.0.3
INTERNET=eth0
LOOPBACK_INTERFACE=lo
SUBNET_BASE=192.168.0/24
LOOPBACK=127.0.0.0/8
CLASS_A=10.0.0.0/8
CLASS_B=172.16.0.0/12
CLASS_C=192.168.0.0/16
CLASS_D_MULTICAST=224.0.0.0/4
CLASS_E_RESERVED_NET=240.0.0.0/5

iptables --flush
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

iptables --policy INPUT DROP
iptables --policy OUTPUT DROP
iptables --policy FORWARD DROP

iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -A INPUT -i $INTERNET -s $IPADDR -j DROP

iptables -A INPUT -i $INTERNET -s $CLASS_A -j DROP
iptables -A INPUT -i $INTERNET -s $CLASS_B -j DROP
iptables -A INPUT -i $INTERNET -s $CLASS_C -j DROP
iptables -A INPUT -i $INTERNET -s $LOOPBACK -j DROP

optimization:
1. loopback rules first
2. forward rules first
3. use state and connection-tracking modules to bypass the firewall for established connections
4. combine rules to standard tcp client-server connections to a single rule using port lists
5. place rules for heavy traffic services as early  as possible

iptables -L

