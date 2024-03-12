### Centos install

```
yum -y install postfix opendkim
```

### rocky install
```
# dnf install -y postfix opendkim opendkim-tools
```

cd /etc/postfix 
vi main.cf

 ```
### Postfix setting
queue_directory = /var/spool/postfix
command_directory = /usr/sbin
daemon_directory = /usr/libexec/postfix
data_directory = /var/lib/postfix
mail_owner = postfix
myhostname = mail2.naver.com
mydomain = mail2.naver.com
myorigin = $mydomain
inet_interfaces = all
inet_protocols = ipv4
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
unknown_local_recipient_reject_code = 550
smtpd_client_restrictions = permit_mynetworks, permit
mynetworks_style = class
mynetworks = 192.168.124.0/23, 58.228.236.0/24, 110.10.90.0/26, 175.126.124.64/26, 192.168.122.0/24, 192.168.127.0/24, 172.17.0.0/16 127.0.0.1, 192.168.246.0/24, 192.168.247.0/24
smtpd_recipient_restrictions = permit_mynetworks,reject_unauth_destination
relay_domains = $mydestination
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
debug_peer_level = 2
debugger_command =
         PATH=/bin:/usr/bin:/usr/local/bin:/usr/X11R6/bin
         ddd $daemon_directory/$process_name $process_id & sleep 5
sendmail_path = /usr/sbin/sendmail.postfix
newaliases_path = /usr/bin/newaliases.postfix
mailq_path = /usr/bin/mailq.postfix
setgid_group = postdrop
html_directory = no
manpage_directory = /usr/share/man
sample_directory = /usr/share/doc/postfix-2.10.1/samples
readme_directory = /usr/share/doc/postfix-2.10.1/README_FILES
 
### Opendkim setting
milter_default_action = accept
milter_protocol = 6
smtpd_milters = inet:127.0.0.1:8891
non_smtpd_milters = $smtpd_milters
``` 
 
 
# cat /etc/opendkim.conf
```
PidFile /var/run/opendkim/opendkim.pid
Mode    sv
Syslog  yes
SyslogSuccess   yes
LogWhy  yes
UserID  opendkim:opendkim
Socket inet:8891@localhost
Umask   002
SendReports     yes
SoftwareHeader  yes
Canonicalization        relaxed/relaxed
Selector        mail2
MinimumKeyBits  1024
KeyTable                /etc/opendkim/KeyTable
SigningTable            refile:/etc/opendkim/SigningTable
ExternalIgnoreList      refile:/etc/opendkim/TrustedHosts
InternalHosts           refile:/etc/opendkim/TrustedHosts
OversignHeaders From
``` 
 
# cd /etc/opendkim
```
[root@xc-mail02 opendkim]# ll
total 12
drwxr-x--- 3 opendkim opendkim   31 Dec  3 19:45 keys
-rw-r----- 1 opendkim opendkim  437 Dec  4 10:49 KeyTable
-rw-r----- 1 opendkim opendkim 1266 Dec  3 20:33 SigningTable
-rw-r----- 1 opendkim opendkim  540 Dec  4 11:15 TrustedHosts
```
 
# cat KeyTable
```
#default._domainkey.example.com example.com:default:/etc/opendkim/keys/default.private
mail2._domainkey.naver.com naver.com:mail2:/etc/opendkim/keys/mail2.naver.com/mail2.private
```
 
# cat SigningTable
```
#example.com default._domainkey.example.com
*@naver.com   mail2._domainkey.naver.com
```
 
# cat TrustedHosts
```
127.0.0.1
58.228.236.0/24
175.126.124.64/26
110.10.90.0/26
192.168.124.0/24
192.168.125.0/24
192.168.122.0/24
192.168.123.0/24
192.168.127.0/24
*.naver.com
```
 
# cd /etc/opendkim/keys
```
mkdir mail2.naver.com
 
cd mail2.naver.com
 
opendkim-genkey -D /etc/opendkim/keys/mail2.naver.com -d naver.com -s mail2
 
[root@xc-mail02 mail2.naver.com]# ll
total 8
-rw------- 1 opendkim opendkim 887 Dec  3 20:30 mail2.private
-rw------- 1 opendkim opendkim 311 Dec  3 20:30 mail2.txt
```
 
# cat mail2.private
```
-----BEGIN RSA PRIVATE KEY-----
MIICXAIBAAKBgQDB5vKi0UcHjqE4ojAAMwv9k29JHBYK51u7Xg9uyfJqnp0XY4ot
~~
-----END RSA PRIVATE KEY-----
```
 
# cat mail2.txt ==> Cloudflare dns에 txt로 추가 해야함
```
mail2._domainkey        IN      TXT     ( "v=DKIM1; k=rsa; " "p=MIGfMA0GCSqGSDAQAB" )  ; ----- DKIM key mail2 for naver.com
```
 
# Cloudflare DNS 등록
# A record 생성
mailx.naver.com 175.126.124.12x
 
# txt 생성 (위 mail2.txt 참고하여 등록)
mailx._domainkey v=DKIM1; k=rsa; " "p=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
 
# CloudFlare의 TXT naver.com SPF에 IP추가 등록
v=spf1 ip4:111.111.111.111 ip4:111.111.111.112 ip4:111.111.111.113 ip4:111.111.111.114 ip4:[신규 IP] -all

 
# nslookup으로 A record, domainkey, spf 확인
set query=txt
 
systemctl enable postfix
systemctl enable opendkim
 
systemctl start postfix
systemctl start opendkim
 
### dkim test
# opendkim-testkey -d
