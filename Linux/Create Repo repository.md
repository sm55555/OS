

#### 1. Repo 서버에 웹서버 ex nginx 를 설치

#### 2. 하위폴더를 만들고 아래 명령어로 받아준다. 여기선 /data

```
rsync  -avrt --progress rsync://mirror.centos.org/ /data/rocky/
```

#### 3. client 세팅

hosts 파일 Repo 서버 주소 ex) mirro.centos.org

vi /etc/hosts
```
111.222.333.444 mirror.centos.org
```

/etc/yum.repos.d에서 url 변경

```
[base]
name=CentOS-$releasever - Base
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
baseurl=http://111.222.333.444/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
released updates 
```
