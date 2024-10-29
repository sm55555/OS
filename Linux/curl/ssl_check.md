
nginx나 apache에 있는 ServerName을 활용하여 남은 인증서 기간 확인가능

예를들어 test.com이라는 사이트가 있을 시 해당 서버 내에서

```
curl -v -k --resolve test.com:443:127.0.0.1 https://test.com 2>&1
```

### openssl 사용법 (web server usin 443)

```
echo '' | openssl s_client -connect localhost:443 openssl x509 -noout -dates
```

### openssl 사용법 (sftp)

```
echo '' | openssl s_client -connect localhost:21 -startls ftp 2>/dev/null | openssl x509 -noout -enddates
```
