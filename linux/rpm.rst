rpm
==============================


rpm install without being root
------------------------------

::

    rpm --initdb --dbpath /home/username/local/lib/rpm
    rpm --dbpath /home/username/local/lib/rpm \
     --relocate /usr=/home/username/local --nodeps -ivh package.rpm
