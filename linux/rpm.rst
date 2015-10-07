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




