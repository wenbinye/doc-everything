chatroom
==============================

Swoole\Server\Socket->run()
$socket = new Swoole\Socket\Swoole;
$client = new \socket\Server;

$this->serv->on('Start', array($this->client, 'onStart'));
$this->serv->on('Connect', array($this->client, 'onConnect'));
$this->serv->on('Receive', array($this->client, 'onReceive'));
$this->serv->on('Close', array($this->client, 'onClose'));
$handlerArray = array(
'onTimer', 
'onWorkerStart', 
'onWorkerStop', 
'onTask', 
'onFinish',
);
