什么是 LDAP
==============================

LDAP Lightweight Directory Access Protocol

LDAP 是基于 entry 信息模型，entry 是一组有全局唯一的 Distinguished Name 的属性。
每个 entry 的属性有一个类型和一个或多个值。 类型例如：cn = common name, mail

DN 格式 rfc4514

rdn: relative distinguished name
dit: directory information tree

dc: domain component

ldif: LDAP interchange format

schemas:
 person
 organizationalPersion
 inetOrgPersion

oid: Object IDentifier

olcObjectClasses:
 unique OID
 NAME
 DESC
 SUP
 MUST
 MAY

objectIdentifier 用于创建 OID 别名

搜索邮箱以 m 开头：
Base DN
Scope
Attributes
Filter

ldif 格式
==============================

objectClass

如果有非 ASCII 字符，需要使用 base64 编码，使用两个冒号：：

documentTitle:: bW9uYWRvbG9neQ==


Root DSE : Root D

修改密码：

ldappasswd -D 'cn=admin,dc=phoenixos,dc=com' -w Ei2bei1e -S 'cn=Ye Wenbin,ou=Users,dc=phoenixos,dc=com'

ldap pam
==============================

apt-get install ldap-auth-client nscd
auth-client-config -t nss -p lac_ldap
vi /usr/share/pam-configs/mkhomedir

Name: active mkhomedir
Default: yes
Priority: 900
Session-Type: Additional
Session:
  required pam_mkhomedir.so umask=0022 skel=/etc/skel

pam-auth-update
/etc/init.d/nscd restart
getent passwd
su - mike

http://www.zytrax.com/books/ldap/
https://www.youtube.com/watch?v=l0e8rG0mku8

config
==============================

ldapadd -H ldapi:/// -f /etc/ldap/schema/ppolicy.ldif

ppolicy

syncrepl rid=123
provider=ldap://ldap.domain.com:389
type=refreshOnly
interval=00:00:01:00
searchbase="dc=mydomain,dc=com"
scope=sub
attrs="*"
schemachecking=off
bindmethod=simple
binddn="cn=admin,dc=phoenixos,dc=com"
credentials=password

rid = replica id can be any thing numberic


https://www.youtube.com/watch?v=qVkxcy17Gls


password hash
------------------------------

function check_password($password, $hash)
{
    if ($hash == '') // no password
    {
        //echo "No password";
        return FALSE;
    }

    if ($hash{0} != '{') // plaintext password
    {
        if ($password == $hash)
            return TRUE;
        return FALSE;
    }

    if (substr($hash,0,7) == '{crypt}')
    {
        if (crypt($password, substr($hash,7)) == substr($hash,7))
            return TRUE;
        return FALSE;
    }
    elseif (substr($hash,0,5) == '{MD5}')
    {
        $encrypted_password = '{MD5}' . base64_encode(md5( $password,TRUE));
    }
    elseif (substr($hash,0,6) == '{SHA1}')
    {
        $encrypted_password = '{SHA}' . base64_encode(sha1( $password, TRUE ));
    }
    elseif (substr($hash,0,6) == '{SSHA}')
    {
        $salt = substr(base64_decode(substr($hash,6)),20);
        $encrypted_password = '{SSHA}' . base64_encode(sha1( $password.$salt, TRUE ). $salt);
    }
    else
    {
        echo "Unsupported password hash format";
        return FALSE;
    }

    if ($hash == $encrypted_password)
        return TRUE;

    return FALSE;
}

配置文件
==============================

sudo ldapsearch -Y EXTERNAL  -H ldapi:// -LLL -b 'cn=config'

ssl/tls 支持
==============================

http://www.openldap.org/faq/data/cache/185.html

  cd /var/myca
  CA.sh -newca
  openssl req -new -nodes -keyout newreq.pem -out newreq.pem
  CA.sh -sign
  cp cacert.pem /usr/local/etc/openldap/cacert.pem
  mv newcert.pem /usr/local/etc/openldap/servercrt.pem
  mv newreq.pem /usr/local/etc/openldap/serverkey.pem
  chmod 600 /usr/local/etc/openldap/serverkey.pem

  TLSCACertificateFile /usr/local/etc/openldap/cacert.pem
  TLSCertificateFile /usr/local/etc/openldap/servercrt.pem
  TLSCertificateKeyFile /usr/local/etc/openldap/serverkey.pem

centos
==============================

yum install openldap-servers openldap-clients
mkdir /var/cacerts
cd /var/cacerts
/etc/pki/tls/misc/CA -newca
openssl req -new -nodes -keyout newreq.pem -out newreq.pem
/etc/pki/tls/misc/CA -sign
cp /etc/pki/CA/cacert.pem .
mv newreq.pem serverkey.pem
mv newcert.pem servercrt.pem
cp *.pem /etc/openldap/certs/
chmod 600 /etc/openldap/certs/serverkey.pem

配置文件：
#
# See slapd.conf(5) for details on configuration options.
# This file should NOT be world readable.
#

include		/etc/openldap/schema/core.schema
include		/etc/openldap/schema/cosine.schema
include		/etc/openldap/schema/nis.schema
include		/etc/openldap/schema/inetorgperson.schema

# include		/etc/openldap/schema/corba.schema
# include		/etc/openldap/schema/duaconf.schema
# include		/etc/openldap/schema/dyngroup.schema
# include		/etc/openldap/schema/java.schema
# include		/etc/openldap/schema/misc.schema
# include		/etc/openldap/schema/openldap.schema
# include		/etc/openldap/schema/ppolicy.schema
# include		/etc/openldap/schema/collective.schema

# Allow LDAPv2 client connections.  This is NOT the default.
# allow bind_v2

# Do not enable referrals until AFTER you have a working directory
# service AND an understanding of referrals.
#referral	ldap://root.openldap.org

pidfile		/var/run/openldap/slapd.pid
argsfile	/var/run/openldap/slapd.args

# Load dynamic backend modules
# - modulepath is architecture dependent value (32/64-bit system)
# - back_sql.la overlay requires openldap-server-sql package
# - dyngroup.la and dynlist.la cannot be used at the same time

# modulepath /usr/lib/openldap
# modulepath /usr/lib64/openldap

moduleload accesslog.la
# moduleload auditlog.la
# moduleload back_sql.la
# moduleload chain.la
# moduleload collect.la
# moduleload constraint.la
# moduleload dds.la
# moduleload deref.la
# moduleload dyngroup.la
# moduleload dynlist.la
# moduleload memberof.la
# moduleload pbind.la
# moduleload pcache.la
# moduleload ppolicy.la
# moduleload refint.la
# moduleload retcode.la
# moduleload rwm.la
# moduleload seqmod.la
# moduleload smbk5pwd.la
moduleload sssvlv.la
moduleload syncprov.la
# moduleload translucent.la
# moduleload unique.la
# moduleload valsort.la

# The next three lines allow use of TLS for encrypting connections using a
# dummy test certificate which you can generate by running
# /usr/libexec/openldap/generate-server-cert.sh. Your client software may balk
# at self-signed certificates, however.
TLSCACertificateFile /etc/openldap/certs/cacert.pem
TLSCertificateKeyFile /etc/openldap/certs/serverkey.pem
TLSCertificateFile /etc/openldap/certs/servercrt.pem
TLSVerifyClient try

# Sample security restrictions
#	Require integrity protection (prevent hijacking)
#	Require 112-bit (3DES or better) encryption for updates
#	Require 63-bit encryption for simple bind
# security ssf=1 update_ssf=112 simple_bind=64

# Sample access control policy:
#	Root DSE: allow anyone to read it
#	Subschema (sub)entry DSE: allow anyone to read it
#	Other DSEs:
#		Allow self write access
#		Allow authenticated users read access
#		Allow anonymous users to authenticate
#	Directives needed to implement policy:
# access to dn.base="" by * read
# access to dn.base="cn=Subschema" by * read
# access to *
#	by self write
#	by users read
#	by anonymous auth
#
# if no access controls are present, the default policy
# allows anyone and everyone to read anything but restricts
# updates to rootdn.  (e.g., "access to * by * read")
#
# rootdn can always read and write EVERYTHING!

# enable on-the-fly configuration (cn=config)
database config
access to *
	by dn.exact="gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth" manage
	by * none

# enable server status monitoring (cn=monitor)
database monitor
access to *
	by dn.exact="gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth" read
        by dn.exact="cn=admin,dc=phoenixos,dc=com" read
        by * none

#######################################################################
# database definitions
#######################################################################

database	hdb
suffix		"dc=phoenixos,dc=com"
checkpoint	1024 15
rootdn		"cn=admin,dc=phoenixos,dc=com"
rootpw {SSHA}qaHIgDf5fePmEhDzKg7o4VCf/7dYeBgO
# Cleartext passwords, especially for the rootdn, should
# be avoided.  See slappasswd(8) and slapd.conf(5) for details.
# Use of strong authentication encouraged.
# rootpw		secret
# rootpw		{crypt}ijFYNcSNctBYg

# The database directory MUST exist prior to running slapd AND 
# should only be accessible by the slapd and slap tools.
# Mode 700 recommended.
directory	/var/lib/ldap
# For the Debian package we use 2MB as default but be sure to update this
# value if you have plenty of RAM
dbconfig set_cachesize 0 2097152 0

# Sven Hartge reported that he had to set this value incredibly high
# to get slapd running at all. See http://bugs.debian.org/303057 for more
# information.

# Number of objects that can be locked at the same time.
dbconfig set_lk_max_objects 1500
# Number of locks (both requested and granted)
dbconfig set_lk_max_locks 1500
# Number of lockers
dbconfig set_lk_max_lockers 1500

# Indices to maintain for this database
index objectClass                       eq,pres
index ou,cn,mail,surname,givenname      eq,pres,sub
index uidNumber,gidNumber,loginShell    eq,pres
index uid,memberUid                     eq,pres,sub
index nisMapName,nisMapEntry            eq,pres,sub
index entryCSN,entryUUID                eq

# Save the time that the entry gets modified, for database #1
lastmod         on

access to attrs=userPassword,shadowLastChange
        by dn="cn=admin,dc=phoenixos,dc=com" write
        by anonymous auth
        by self write
        by * none

access to dn.base="" by users read

access to *
        by dn="cn=admin,dc=phoenixos,dc=com" write
        by users read
        by anonymous none

overlay syncprov
syncprov-checkpoint 50 10
syncprov-sessionlog 100

# Replicas of this database
#replogfile /var/lib/ldap/openldap-master-replog
#replica host=ldap-1.example.com:389 starttls=critical
#     bindmethod=sasl saslmech=GSSAPI
#     authcId=host/ldap-master.example.com@EXAMPLE.COM


初始数据：

dn: dc=phoenixos,dc=com
dc: phoenixos
objectClass: dcObject
objectClass: organization
o: phoenixos.com

dn: ou=System,dc=phoenixos,dc=com
objectClass: organizationalUnit
ou: System

dn: cn=syncrepl,ou=System,dc=phoenixos,dc=com
objectClass: simpleSecurityObject
objectClass: account
cn: syncrepl
ou: System
userPassword: {SSHA}9SYD7CKHxJ+SIqdVpEVOlPXfp+YfbzbM
description: SyncRepl account

dn: ou=Groups,dc=phoenixos,dc=com
objectClass: organizationalUnit
ou: Groups

dn: cn=staff,ou=Groups,dc=phoenixos,dc=com
objectClass: posixGroup
cn: staff
gidNumber: 2000

dn: ou=Users,dc=phoenixos,dc=com
objectClass: organizationalUnit
ou: Users

dn: uid=yewenbin,ou=Users,dc=phoenixos,dc=com
objectclass: inetOrgPerson
objectclass: posixAccount
objectclass: shadowAccount
uid: yewenbin
ou: Users
cn: Ye Wenbin
sn: Ye
givenName: Wenbin
displayName:: 5Y+25paH5b2s
userPassword: {SSHA}vOJDdK8F+8CHKbkDmhSQzAxKs07tS1gf
mail: yewenbin@phoenixos.com
uidNumber: 2000
gidNumber: 2000
loginShell: /bin/bash
homeDirectory: /home/ywb
telephoneNumber: 18600919133

导入配置文件：

sed -i 's/SLAPD_LDAP=yes/SLAPD_LDAP=no/' /etc/sysconfig/ldap
sed -i 's/SLAPD_LDAPS=no/SLAPD_LDAPS=yes/' /etc/sysconfig/ldap
cp slapd.conf /etc/openldap/slapd.conf
rm -rf /etc/openldap/slapd.d/*
# 如果出现错误
# 5673dfd6 hdb_db_open: database "dc=phoenixos,dc=com": db_open(/var/lib/ldap/id2entry.bdb) failed: No such file or directory (2).
chown -R ldap. /var/lib/ldap
service slapd start
service slapd stop
# 注意最后 / 是需要的
sudo -u ldap slaptest -f /etc/openldap/slapd.conf -F /etc/openldap/slapd.d/
service slapd start

