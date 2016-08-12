nginx 配置
==============================

server {
    listen       80;
    server_name  gerrit.ywb.chaozhuo.net;
    auth_basic "Gerrit Code Review";
    auth_basic_user_file "/home/ywb/local/etc/htpasswd";

    location / {
        include /etc/nginx/proxy_params;
        proxy_pass http://192.168.1.189:8811;
    }
}

ldap 配置
====================================

[auth]
	type = LDAP
[ldap]
    server = ldap://192.168.1.189
    accountBase = ou=Users,dc=phoenixos,dc=com
    groupBase = ou=Users,dc=phoenixos,dc=com
    accountPattern = (&(objectClass=inetOrgPerson)(uid=${username}))
    accountFullName = ${cn}

bin/gerrit.war
etc/secure.config
etc/ssh_host_key
index/gerrit_index.config
