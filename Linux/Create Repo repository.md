

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


### 도커 올리고하는방법

baseos, appstream, extras

### Rocky linux 다운 후 도커 마운트

```
docker run -v /data/rocky:/mnt --name rockylinux -d rockylinux/rockylinux sleep infinity
```

### repo 설정 여기선 appstream

reposync -g -m --repoid=appstream --download-metadata --newest-only -p=/mnt/

### create repo

createrepo /mnt/appstream


