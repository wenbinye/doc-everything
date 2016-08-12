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

repository 配置
------------------------------


composer 代码分析
------------------------------

command 注册 : Application::__construct, getDefaultCommands

Composer\Console\Application::run


toran 代码分析
------------------------------

router = /home/ywb/src/php/toran/src/Toran/ProxyBundle/Resources/config/routing.yml

curld http://toran.phoenixstudio.org/repo/packagist/p/wenbinye/php-phalconx.json

/home/ywb/src/php/toran/src/Toran/ProxyBundle/Controller/ProxyController.php

$proxy = Toran\ProxyBundle\Service\Proxy
$filename = wenbinye/php-phalconx.json

$proxy->cacheDir = /home/ywb/src/php/toran/app/toran/cache/packagist

http://toran.phoenixstudio.org/repositories/0-24ce30a8fdb11ce4ee86dafbb0b48d1239fd9c59
/home/ywb/src/php/toran/src/Toran/ProxyBundle/Controller/RepoController.php

$repo = Toran\ProxyBundle\Model\Repository
配置 /home/ywb/src/php/toran/app/toran/config.yml

版本格式
------------------------------

tags ：
1.0.0
v1.0.0
1.10.5-RC1
v4.4.4beta2
v2.0.0-alpha
v2.0.4-p1

分支：
1.x   => 1.x-dev
1.0   => 1.0.x-dev
1.1.x => 1.1.x-dev
master => dev-master
develop => dev-develop
