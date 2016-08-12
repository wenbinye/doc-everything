piwik
==============================

解决 load data infile 问题：
1. 需要安装 php5-mysqlnd
2. /etc/mysql/my.cnf 需要配置 [mysqld] local-infile

mysql 客户端测试需要配置 [client] local-infile=1

LOAD DATA LOCAL INFILE '/home/ywb/src/php/piwik/tmp/assets/piwik_option-1ebb504cc0636c3daf6b327d85364e0c.csv'
INTO TABLE piwik_option 
FIELDS TERMINATED BY '\t' ENCLOSED BY '"' ESCAPED BY '\\' LINES TERMINATED BY '\r\n' (option_name,option_value);

导入日志
==============================

./import_logs.py --url=http://localhost/piwik/ --idsite=2 --recorders=4 --enable-http-errors --enable-http-redirects --enable-static --enable-bots --log-format-name=ncsa_extended --login admin --password admin2016 /tmp/bbs.log

./misc/log-a/import_logs.py --url=http://localhost/piwik/ -ddd --dry-run --idsite=1 --recorders=4 --enable-http-errors --log-format-regex='\S+\s+\S+\s+(?P<userid>\S+)\s+\[(?P<date>.*?)\s+(?P<timezone>.*?)\]\s+"\S+\s+(?P<path>.*?)\s+\S+"\s+(?P<status>\S+)\s+(?P<length>\S+)\s+"(?P<referrer>.*?)"\s+"(?P<user_agent>.*?)"\s+"(?P<ip>\S+)"' /tmp/os.log

client
==============================

http://developer.piwik.org/api-reference/PHP-Piwik-Tracker

https://github.com/piwik/piwik-php-tracker

自定义变量和自定义维度
==============================

user_status=LoggedIn

android sdk
==============================

https://github.com/piwik/piwik-sdk-android

{
   "requests" : [
      "?uid=6af62572-a587-4f59-82d3-7f66d48a5040&apiv=1&_idvc=1&e_a=downloaded&idsite=3&res=720x1280&send_image=0&cdt=2016-02-18%2016%3A35%3A44%2B0800&download=http%3A%2F%2Fcom.piwik.demo%3A1%2F5B030417B60D3B0E8872D97E8EED092C&urlref=unknown&lang=zh&url=http%3A%2F%2Fcom.piwik.demo%2Fapplication%2Fdownloaded&e_c=Application&country=CN&rec=1&_id=23ba1a13c6ea4f13&new_visit=1&action_name=application%2Fdownloaded&ua=Dalvik%2F1.6.0%20%28Linux%3B%20U%3B%20Android%204.3%3B%20Galaxy%20Nexus%20Build%2FJWR66Y%29&rand=82949&_idts=1455784544",
      "?uid=6af62572-a587-4f59-82d3-7f66d48a5040&apiv=1&_idvc=1&idsite=3&res=720x1280&send_image=0&cdt=2016-02-18%2016%3A36%3A30%2B0800&_viewts=1455784544&lang=zh&url=http%3A%2F%2Fcom.piwik.demo%2F&country=CN&rec=1&_id=23ba1a13c6ea4f13&new_visit=1&action_name=Main%20screen&ua=Dalvik%2F1.6.0%20%28Linux%3B%20U%3B%20Android%204.3%3B%20Galaxy%20Nexus%20Build%2FJWR66Y%29&rand=61888&_idts=1455784544",
      "?uid=6af62572-a587-4f59-82d3-7f66d48a5040
apiv=1
_idvc=1
idsite=3
res=720x1280
send_image=0
cdt=2016-02-18 16:36:37+0800
_viewts=1455784544
lang=zh
url=http://com.piwik.demo/
country=CN
rec=1
_id=23ba1a13c6ea4f13
new_visit=1
action_name=Main screen
ua=Dalvik/1.6.0 (Linux; U; Android 4.3; Galaxy Nexus Build/JWR66Y)
rand=49388
_idts=1455784544",
      "?uid=6af62572-a587-4f59-82d3-7f66d48a5040
apiv=1
_idvc=1
idsite=3
res=720x1280
ec_st=10.00
ec_tx=20.00
ec_id=8358.558877734644
idgoal=0
send_image=0
cdt=2016-02-18 16:37:04+0800
_viewts=1455784544
ec_dt=5.00
lang=zh
url=http://com.piwik.demo/
country=CN
ec_items=[]
rec=1
ec_sh=30.00
_id=23ba1a13c6ea4f13
new_visit=1
ua=Dalvik/1.6.0 (Linux; U; Android 4.3; Galaxy Nexus Build/JWR66Y)
rand=58666
_idts=1455784544
revenue=100.00",
      "?
   ]
}

_id=23ba1a13c6ea4f13
_idts=1455784544
_idvc=1
action_name=application/downloaded
apiv=1
cdt=2016-02-18 16:35:44+0800
country=CN
download=http://com.piwik.demo:1/5B030417B60D3B0E8872D97E8EED092C
e_a=downloaded
e_c=Application
idsite=3
lang=zh
new_visit=1
rand=82949
rec=1
res=720x1280
send_image=0
ua=Dalvik/1.6.0 (Linux; U; Android 4.3; Galaxy Nexus Build/JWR66Y)
uid=6af62572-a587-4f59-82d3-7f66d48a5040
url=http://com.piwik.demo/application/downloaded
urlref=unknown

_id  => VISITOR_ID
_idts => FIRST_VISIT_TIMESTAMP
_idvc => TOTAL_NUMBER_OF_VISITS
action_name
apiv  => API_VERSION always 1
cdt = DATETIME_OF_REQUEST
e_a = event action
e_c = event category
download = 下载文件名
rec = 1
res = resolution

_id=23ba1a13c6ea4f13
_idts=1455784544
_idvc=1
_viewts=1455784544
action_name=Main screen
apiv=1
cdt=2016-02-18 16:36:30+0800
country=CN
idsite=3
lang=zh
new_visit=1
rand=61888
rec=1
res=720x1280
send_image=0
ua=Dalvik/1.6.0 (Linux; U; Android 4.3; Galaxy Nexus Build/JWR66Y)
uid=6af62572-a587-4f59-82d3-7f66d48a5040
url=http://com.piwik.demo/

_viewts = PREVIOUS_VISIT_TIMESTAMP

_id=23ba1a13c6ea4f13
_idts=1455784544
_idvc=1
_viewts=1455784544
action_name=Settings
apiv=1
cdt=2016-02-18 16:37:19+0800
country=CN
idsite=3
lang=zh
new_visit=1
rand=26411
rec=1
res=720x1280
send_image=0
ua=Dalvik/1.6.0 (Linux; U; Android 4.3; Galaxy Nexus Build/JWR66Y)
uid=6af62572-a587-4f59-82d3-7f66d48a5040
url=http://com.piwik.demo/Settings


POST http://piwik.ywb.chaozhuo.net/piwik.php HTTP/1.1
Content-Type: application/json
charset: utf-8
User-Agent: Dalvik/1.6.0 (Linux; U; Android 4.3; Galaxy Nexus Build/JWR66Y)
Host: piwik.ywb.chaozhuo.net
Connection: Keep-Alive
Accept-Encoding: gzip
Content-Length: 644

{"requests":["?uid=2fb99038-b253-40e8-861f-736a83373fb6&apiv=1&idsite=3&rec=1&_id=30489f8a8c1f4923&send_image=0&action_name=Main%20screen&cdt=2016-02-25%2015%3A34%3A56%2B0800&rand=41568&url=http%3A%2F%2Fcom.piwik.demo%2F","?uid=2fb99038-b253-40e8-861f-736a83373fb6&apiv=1&idsite=3&rec=1&_id=30489f8a8c1f4923&send_image=0&action_name=Main%20screen&cdt=2016-02-25%2015%3A34%3A58%2B0800&rand=97992&url=http%3A%2F%2Fcom.piwik.demo%2F","?uid=2fb99038-b253-40e8-861f-736a83373fb6&apiv=1&idsite=3&rec=1&_id=30489f8a8c1f4923&send_image=0&action_name=Settings&cdt=2016-02-25%2015%3A35%3A01%2B0800&rand=93989&url=http%3A%2F%2Fcom.piwik.demo%2FSettings"]}

heartbeat
==============================

_paq.push(['enableHeartBeatTimer']);
http://fenxi.chaozhuo.net/piwik.php?ping=1&idsite=4&rec=1&r=317545&h=9&m=54&s=33&url=http%3A%2F%2Fos.chaozhuo.net%2F&_id=105c56a40968369c&_idts=1457402035&_idvc=1&_idn=0&_refts=0&_viewts=1457402035&send_image=0&pdf=1&qt=0&realp=0&wma=0&dir=0&fla=1&java=0&gears=0&ag=0&cookie=1&res=1920x1080&gt_ms=33
