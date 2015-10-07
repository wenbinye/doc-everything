nginx
------------------------------

brew install nginx
sudo nginx

配置文件 /usr/local/etc/nginx/nginx.conf

sudo lsof -n -i4TCP:80

mysql
---------------------------------

brew install mysql
chown -R _mysql /usr/local/var/mysql
sudo mysql.server start

php
------------------------------

curl -s http://php-osx.liip.ch/install.sh | bash -s 5.5

bunzip2 -c /Users/ywb/local/softwares/php-5.5-10.10-frontenddev-5.5.25-20150515-095348.tar.bz2  | tar xf -C /usr/local -
