## cent OS nginx 설치 방법

### Nignx 저장소 추가

```
[test@localhost ~]$ sudo vi /etc/yum.repos.d/nginx.repo
```

### /etc/yum.repos.d

```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```

### Install 

```
[test@localhost ~]$ sudo yum install -y nginx
```
