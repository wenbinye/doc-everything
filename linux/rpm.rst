rpm
==============================


rpm install without being root
------------------------------

::

    rpm --initdb --dbpath $HOME/var/rpm
    rpm --dbpath /home/username/local/lib/rpm \
     --relocate /usr=/home/username/local --nodeps -ivh package.rpm

rpmbuild 自动添加 Requires
------------------------------

You can turn off automatic dependency processing in the .spec with ::

   AutoReqProv: no

http://superuser.com/questions/109107/how-do-i-prevent-rpmbuild-form-injecting-requirements-into-rpm-package

disable fastestmirror
------------------------------

edit /etc/yum/pluginconf.d/fastestmirror.conf , change enabled=1 to enabled=0

http://www.zedt.eu/tech/linux/disable-yum-fastestmirror-plugin-on-centos/

yum 变量
------------------------------
http://blog.sina.com.cn/s/blog_828e50020101hd6r.html

http://bencane.com/2013/04/15/creating-a-local-yum-repository/
http://linuxsysconfig.com/2013/04/create-a-yum-repository-with-custom-gpg-signed-packages/
http://giovannitorres.me/how-to-setup-an-rpm-signing-key.html

http://aaronhawley.livejournal.com/10615.html

 $ ./rpm-sign.exp PACKAGE-FILE
Here's the script.

  #!/usr/bin/expect -f
  
  ### rpm-sign.exp -- Sign RPMs by sending the passphrase.
   
  spawn rpm --addsign {*}$argv
  expect -exact "Enter pass phrase: "
  send -- "Secret passphrase\r"
  expect eof

http://mirrorlist.centos.org/?release=6&arch=x86_64&repo=os
https://mirrors.fedoraproject.org/metalink?repo=epel-6&arch=x86_64
