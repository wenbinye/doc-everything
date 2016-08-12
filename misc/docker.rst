curl -L https://get.docker.com/ubuntu/  | sudo sh

sudo docker info

sudo start docker
sudo stop docker

sudo docker run -i -t ubuntu /bin/bash
sudo docker ps -a
sudo docker start jolly_kilby
sudo docker attach jolly_kilby

sudo docker run --name jolly_kilby  -i -t ubuntu /bin/bash

sudo docker run --name daemon_dave -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"

sudo docker rm 80430f8d0921

sudo docker images

https://github.com/ngineered/nginx-php-fpm


https://github.com/sameersbn/docker-gitlab

https://docs.docker.com/installation/ubuntulinux/#giving-non-root-access
http://askubuntu.com/questions/477551/how-can-i-use-docker-without-sudo

Add the docker group if it doesn't already exist:

sudo groupadd docker
Add the connected user "${USER}" to the docker group. Change the user name to match your preferred user:

sudo gpasswd -a ${USER} docker
Restart the Docker daemon:

sudo service docker restart
If you are on Ubuntu 14.04 and up use docker.io instead:

sudo service docker.io restart
Either do a newgrp docker or log out/in to activate the changes to groups.


docker log -f --tail=1 name

linking
==============================
container 名字用途：
1. 命令使用
2. docker 引用


http://mirrors.163.com/.help/centos.html


docker rmi $(docker images -q -f "dangling=true")
docker rm $(docker ps -q -f "status=exited")

docker exec -it [container-id] bash

dockerfiles
==============================

tengine 配置文件：

* addon.d 插件，如 php
* conf.d 所有网站配置
* host.d 虚拟域名配置
* nginx.d http 加载一次
* nginx.conf

nginx.conf ::

    daemon off;
    pid /var/run/nginx.pid;
    user core;
    worker_processes auto;

    events {
            multi_accept on;
            #pcre_jit on;
            use epoll;
            worker_connections 1024;
    }

    http {
            include /usr/local/nginx/conf/nginx.d/*.conf;
            include /usr/local/nginx/conf/host.d/*.conf;
    }

nginx.d 全部内容 ::

    include /usr/local/nginx/conf/mime.types;
    default_type application/octet-stream;
    access_log /data/logs/access.log;
    error_log /data/logs/error.log;
    sendfile on;
    server_names_hash_bucket_size 128;
    tcp_nodelay on;
    tcp_nopush on;
    gzip on;
    gzip_comp_level 9;
    gzip_min_length 256;
    gzip_types application/javascript text/css text/plain text/xml;

host.d 中虚拟域名配置 ::

     server {
             listen 80 default_server;
             root /data/http;
             include /usr/local/nginx/conf/addon.d/default-*.conf;
             include /usr/local/nginx/conf/conf.d/*.conf;
             include /data/config/nginx-*.conf;
     }

docker reading
==============================

https://www.docker.com/products/use-cases
https://medium.com/@ramangupta/why-docker-data-containers-are-good-589b3c6c749e
http://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/
http://container42.com/

http://blog.codeaholics.org/2013/giving-dockerlxc-containers-a-routable-ip-address/
https://github.com/jeroenpeeters/docker-network-containers
http://blog.oddbit.com/2014/08/11/four-ways-to-connect-a-docker/

http://jasonwilder.com/

1. docker 用户



2. network

ip link add virtual0 link eth0 type macvlan mode bridge
dhclient virtual0
ip link set virtual0 up

使用 ip route 获取路由信息：

ip link add virtual0 link eth0 type macvlan mode bridge # address 00:11:22:33:44:55
ip link add virtual0 link eth0 type macvlan mode bridge
ip link set netns $(docker-pid redis) virtual0

nsenter --target $(docker-pid redis) --mount --uts --ipc --net --pid
在 container 运行：
ip link set virtual0 up
ip route del default
ip addr add 192.168.1.207/24 dev virtual0
ip route add default via 192.168.1.1 dev virtual0

ubuntu
---------------------------------

locale-gen en_US.UTF-8
export LANG=en_US.UTF-8

创建可路由的 container
------------------------------

脚本 ::

    #!/bin/bash
    set -ex

    dir=$(dirname $0)
    ip="192.168.1.207"
    mac="26:74:b6:18:74:e6"

    c12id=$(docker-compose -f $dir/docker-compose.yml ps -q gitlab | cut -c 1-12)
    pipework eth0 $c12id $ip/24 $mac

    virtual_if="br$c12id"
    ip link add $virtual_if link eth0 type macvlan mode bridge
    dhclient $virtual_if
    ip route del 192.168.1.0/24 dev $virtual_if

    virtual_ip=$(ip -f inet addr show dev $virtual_if | grep inet | awk '{print $2}' | sed 's#/.*##')
    ip -f inet route add $ip dev $virtual_if

mysql
------------------------------

env:
When you start the mysql image, you can adjust the configuration of the MySQL instance by passing one or more environment variables on the docker run command line. Do note that none of the variables below will have any effect if you start the container with a data directory that already contains a database: any pre-existing database will always be left untouched on container startup.

MYSQL_ROOT_PASSWORD
This variable is mandatory and specifies the password that will be set for the MySQL root superuser account. In the above example, it was set to my-secret-pw.

MYSQL_DATABASE
This variable is optional and allows you to specify the name of a database to be created on image startup. If a user/password was supplied (see below) then that user will be granted superuser access (corresponding to GRANT ALL) to this database.

MYSQL_USER, MYSQL_PASSWORD
These variables are optional, used in conjunction to create a new user and to set that user's password. This user will be granted superuser permissions (see above) for the database specified by the MYSQL_DATABASE variable. Both variables are required for a user to be created.

Do note that there is no need to use this mechanism to create the root superuser, that user gets created by default with the password specified by the MYSQL_ROOT_PASSWORD variable.

MYSQL_ALLOW_EMPTY_PASSWORD
This is an optional variable. Set to yes to allow the container to be started with a blank password for the root user. NOTE: Setting this variable to yes is not recommended unless you really know what you are doing, since this will leave your MySQL instance completely unprotected, allowing anyone to gain complete superuser access.

php-fpm 环境变量
------------------------------

http://l33t.peopleperhour.com/2014/03/13/setting-environment-variables-in-php-fpm-when-using-docker-links/

mount volume when running
==============================


df -P /home/ywb/docker/centos-ldap/data | 
/dev/sda7

weave
==============================

vagrant@weave-gs-01:~$ weave status

        Version: 1.4.1

        Service: router
       Protocol: weave 1..2
           Name: c6:8e:68:e3:fa:7b(weave-gs-01)
     Encryption: disabled
  PeerDiscovery: enabled
        Targets: 0
    Connections: 1 (1 established)
          Peers: 2 (with 2 established connections)
 TrustedSubnets: none

        Service: ipam
         Status: idle
          Range: 10.32.0.0-10.47.255.255
  DefaultSubnet: 10.32.0.0/12

        Service: dns
         Domain: weave.local.
       Upstream: 10.0.2.3
            TTL: 1
        Entries: 0

        Service: proxy
        Address: unix:///var/run/weave/weave.sock

        Service: plugin
     DriverName: weave

vagrant@weave-gs-02:~$ weave status

        Version: 1.4.1

        Service: router
       Protocol: weave 1..2
           Name: 8a:99:0b:64:94:11(weave-gs-02)
     Encryption: disabled
  PeerDiscovery: enabled
        Targets: 1
    Connections: 1 (1 established)
          Peers: 2 (with 2 established connections)
 TrustedSubnets: none

        Service: ipam
         Status: idle
          Range: 10.32.0.0-10.47.255.255
  DefaultSubnet: 10.32.0.0/12

        Service: dns
         Domain: weave.local.
       Upstream: 10.0.2.3
            TTL: 1
        Entries: 0

        Service: proxy
        Address: unix:///var/run/weave/weave.sock
