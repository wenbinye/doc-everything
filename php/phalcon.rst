DI\FactoryDefault
------------------------------

===================  ========================================
service               definition
===================  ========================================
annotations           Phalcon\Annotations\Adapter\Memory
assets                Phalcon\Assets\Manager
cookies               Phalcon\Http\Response\Cookies
crypt                 Phalcon\Crypt
dispatcher            Phalcon\Mvc\Dispatcher
escaper               Phalcon\Escaper
eventsManager         Phalcon\Events\Manager
filter                Phalcon\Filter
flash                 Phalcon\Flash\Direct
flashSession          Phalcon\Flash\Session
modelsManager         Phalcon\Mvc\Model\Manager
modelsMetadata        Phalcon\Mvc\Model\MetaData\Memory
request               Phalcon\Http\Request
response              Phalcon\Http\Response
router                Phalcon\Mvc\Router
security              Phalcon\Security
session               Phalcon\Session\Adapter\Files
sessionBag            Phalcon\Session\Bag
tag                   Phalcon\Tag
transactionManager    Phalcon\Mvc\Model\Transaction\Manager
url                   Phalcon\Mvc\Url
===================  ========================================

model
------------------------------

initialize 只调用一次

useDynamicUpdate(true) 可只在更新字段才调用 update 语句
