### NOT starting grafana-server by default on bootup, please execute
 sudo update-rc.d grafana-server defaults 95 10
### In order to start grafana-server, execute
 sudo service grafana-server start

### NOT starting grafana-server by default on bootup, please execute
 sudo /sbin/chkconfig --add grafana-server
### In order to start grafana-server, execute
 sudo service grafana-server start
  Verifying  : grafana-2.0.2-1.x86_64
