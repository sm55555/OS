## Version Check

```
[root@localhost ~]# httpd -v
Server version: Apache/2.2.15 (Unix)
Server built:   Oct 19 2017 16:43:38
[root@localhost ~]# php -v (안되면 whereis php)
PHP 5.6.29 (cli) (built: Dec  8 2016 08:51:50) 
Copyright (c) 1997-2016 The PHP Group
Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies
```
## 1. httpd.conf 파일 수정

```
[root@localhost ~]# vi /etc/httpd/conf/httpd.conf
 
DirectoryIndex index.html index.html.var // 이 부분 찾아서 아래와 같이 추가
-> DirectoryIndex index.html index.html.var index.php index.php3
 
# If the AddEncoding directives above are commented-out, then you
# probably should define those extensions to indicate media types:
#
AddType application/x-compress .Z
AddType application/x-gzip .gz .tgz // 이 부분 찾아서 아래 2줄 추가 후 저장
AddType application/x-httpd-php .php .html .htm .inc
AddType application/x-httpd-php-source .phps
 
[root@localhost ~]# service httpd restart // httpd 서비스 재시작
Stopping httpd: [  OK  ]
Starting httpd: [  OK  ]
[root@localhost ~]# 
```

## 2. 연동확인

```
[root@localhost ~]# vi /var/www/html/phpinfo.php /* 사용자 마다 디렉토리는 다를 수 있음 */
 
<?php
phpinfo()
?>
```

## 3. 확인

```
[root@localhost ~]# curl "http://localhost/phpinfo.php"
```

