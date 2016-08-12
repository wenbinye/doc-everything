server prepare:
openssl genrsa -desc3 2048 > private/ca.key
openssl req -new -x509 -key private/ca.key -out ca.crt
openssl x509 -in ./ca.crt --dates -noout --issuer

client: 
openssl genrsa -des3 2048 > client.key
openssl req -new -key client.key -out domain.csr

server sign:
openssl ca -in domain.csr -out domain.crt

https://www.youtube.com/watch?v=Gw-Iq9StoXg

无密码：
openssh rsa -in client.key.pass -out client.key


dn:cn=config
changeType: modify
add: olcTLSCACertificateFile
olcTLSCACertificateFile: /etc/ldap/ca.crt
-
add: olcTLSCertificateFile
olcTLSCertificateFile: /etc/ldap/ldap.crt
-
add: olcTLSCertificateKeyFile
olcTLSCertificateKeyFile: /etc/ldap/ldap.key
