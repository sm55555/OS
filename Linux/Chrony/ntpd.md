## ntpd

```
가끔 CentOS 6에 깔려있는 서버들이 있다.

service status ntpd
service start ntpd
service stop ntpd
```

### ntpd 시간 즉시 동기화

```
ntpdate [ip 주소]
```

### ntpd 현황 파악

```
ntpstat && ntpq -pn
```

### /etc/ntp.conf 주의할점

```
restrict default nomodify notrap noquery // 이 설정은 기본으로 모든 권한을 주지 않음을 의미한다. 
```
