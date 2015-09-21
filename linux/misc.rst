xz 文件
------------------------------

创建 ::

   tar cfJ archive.tar.xz files

解压缩 ::

   tar xz archive.tar.xz

菜单安装
------------------------------

#!/bin/sh
xdg-desktop-menu install --mode system "/tmp/jetbrains-idea-ce.desktop"
RV=$?
xdg-desktop-menu forceupdate --mode system
exit $RV

修改时区
------------------------------

cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

rsync 文件
------------------------------

rsync -v -az -e ssh chaozhuo01:rpms .

rsync -av --include="site*.gz" --exclude="*" www:nginx/logs/ nginx

注意 logs/ 是必须的，否则需要使用 --include="logs/site*.gz"

续传文件：

rsync -P -avz -e ssh ookong.com:ubuntu-14.04-amd64.box .
