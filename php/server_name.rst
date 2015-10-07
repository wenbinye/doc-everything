SERVER_NAME vs HTTP_HOST
------------------------------

HTTP_HOST 是与请求相关的，SERVER_NAME 是 web 服务器配置的。
nginx SERVER_NAME 是 server_name 指令的第一个域名。例如 ::

    server {
        listen 80;
        server_name admin-test.tongxinfen.cn admin-test.tongxinfan.com;
        location / {
           proxy_pass http://localhost:8081;
         }
    }
  
无论请求哪个域名，php 中的 ``$_SERVER['SERVER_NAME']`` 值都是 admin-test.tongxinfen.cn。
