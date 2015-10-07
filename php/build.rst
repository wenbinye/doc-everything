Php 编译
==============================

ubuntu 编译
==============================

::

    $ sudo apt-get build-dep php5
    $ sudo aptitude install libt1-dev libmcrypt-dev libreadline-dev
    $ sudo ln -sf x86_64-linux-gnu/gmp.h /usr/include/
    $ ./configure --config-cache \
        --prefix=/home/admin/php \
        --sbindir=/home/admin/php \
        --sysconfdir=/home/admin/php \
        --with-config-file-path=/home/admin/php \
        --with-config-file-scan-dir=/home/admin/php/conf.d \
        --mandir=/home/admin/php/share/man \
        --with-layout=GNU \
        --disable-rpath \
        --disable-cgi \
        --with-readline \
        --enable-pcntl \
        --enable-cli \
        --with-pear \
        --enable-fpm \
        --with-fpm-user=admin \
        --with-fpm-group=admin \
        --enable-mbstring \
        --enable-bcmath \
        --enable-calendar \
        --enable-exif \
        --enable-inline-optimization \
        --enable-intl \
        --enable-mbregex \
        --enable-phar \
        --enable-posix \
        --enable-shmop \
        --enable-soap \
        --enable-sockets \
        --enable-sysvmsg \
        --enable-sysvsem \
        --enable-sysvshm \
        --enable-zip \
        --with-bz2 \
        --with-curl \
        --with-freetype-dir=/usr \
        --with-gd \
        --with-gettext \
        --with-gmp \
        --with-iconv \
        --with-icu-dir=/usr \
        --with-jpeg-dir=/usr \
        --with-layout=PHP \
        --with-libdir=lib64 \
        --with-libxml-dir=/usr \
        --with-mcrypt \
        --with-mhash \
        --with-mysql=mysqlnd \
        --with-mysqli=mysqlnd \
        --with-openssl \
        --with-pdo-mysql=mysqlnd \
        --with-pdo-sqlite \
        --with-png-dir=/usr \
        --with-pspell \
        --with-t1lib=/usr \
        --with-tidy=/usr \
        --with-vpx-dir=/usr \
        --with-xmlrpc \
        --with-xpm-dir=/usr \
        --with-xsl \
        --with-zlib \
        --with-zlib-dir=/usr
   
