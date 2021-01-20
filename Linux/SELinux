# SELinux

리눅스 보안 모듈, 커털 2.6부터 일반적으로 제공 되어 있음 커널 확인은 uname -r

크게 3가지 모드가 있다.

enabled, permissive, disabled

enabled : 활성, 차단 가능
permissive : 켜져는 있지만 안막고, audit에 로그만 남긴다.
disabled : 비활성화


운영 중에는 permissive, enabled만 변경 가능

```
[root@localhost~]# sestatus
```

disabled으로 바꾸려면 etc/sysconfig/selinux 설정에서 변경하고 재부팅



