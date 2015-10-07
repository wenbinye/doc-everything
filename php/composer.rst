composer
==============================

repository 配置
---------------------------------


composer global require "phpunit/phpunit=4.6.*"
composer global require "phpunit/dbunit"

强制代码格式检查
------------------------------

http://tech.zumba.com/2014/04/14/control-code-quality/

创建本地 composer 镜像
------------------------------

http://code.tutsplus.com/tutorials/setting-up-a-local-mirror-for-composer-packages-with-satis--net-36726

http://blog.servergrove.com/2015/04/29/satis-building-composer-repository/

$ php composer.phar create-project composer/satis --stability=dev --keep-vcs 

创建配置文件 mirrored-packages.conf

{
    "name": "NetTuts Composer Mirror",
    "homepage": "http://localhost:4680",

    "repositories": [
        { "type": "vcs", "url": "https://github.com/SynetoNet/monolog" },
        { "type": "composer", "url": "https://packagist.org" }
    ],

    "require": {
        "monolog/monolog": "syneto-dev",
        "mockery/mockery": "*",
        "phpunit/phpunit": "*"
    },
    "require-dependencies": true
}

$ php ./satis/bin/satis build ./mirrored-packages.conf ./packages-mirror

$ php -S localhost:4680 -t ./packages-mirror/

