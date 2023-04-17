#### 1. Repo 서버에 웹서버 ex nginx 를 설치

nginx 설정

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        root /data;
        index repomd.xml;
        
        location / {
                 
          }
        
       }
```

#### 2. 하위폴더를 만들고 아래 명령어로 받아준다. 여기선 /data

```
rsync  -avrt --progress rsync://mirror.centos.org/ /data/rocky/
```

#### 3. client 세팅

hosts 파일 Repo 서버 주소 ex) mirro.centos.org

vi /etc/hosts
```
111.222.333.444 mirror.centos.org
111.222.333.444 dl.rockylinux.org
```

/etc/yum.repos.d에서 url 변경

```
CentOS
[base]
name=CentOS-$releasever - Base
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
baseurl=http://mirror.centos.org/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
released updates 


Rocky
[baseos]
name=Rocky-$releasever - Base
mirrorlist=http://mirror.rockylinux/?release=$releasever&arch=$basearch&repo=os&infra=$infra
baseurl=http://dl.rockylinux.org/centos/$releasever/os/$basearch/
gpgcheck=1
enable=1
countme=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rockyofficial
```

client 서버에서 테스트를 진행해야한다. (특히 centos, rocky) 아래 명령어 결과 후 repomd 관련 내용 출력

```
curl -v http://mirrorlist.centos.org/baseos/repodata/repomd.xml
curl -v http://mirror.rockylinux/baseos/repodata/repomd.xml
```


### 도커 올리고하는방법

baseos, appstream, extras

### Rocky linux 다운 후 도커 마운트

```
docker run -v /data/rocky:/mnt --name rockylinux -d rockylinux/rockylinux sleep infinity
```

### Rockylinux repo 설정

```
reposync -g -m --repoid=appstream --download-metadata --newest-only -p=/mnt/
```

### CentOS repo 설정

```
reposync -g -m --repoid=appstream --download-metadata --newest-only --download_path=/mnt
```

### create repo

createrepo /mnt/appstream

### Error: GPG check FAILED

-g, --gpgcheck
              Remove packages that fail GPG signature checking after
              downloading.  exit status is '1' if at least one package
              was removed.

```
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-centosofficial 

or

g 옵션을 제외
reposync -m --repoid=appstream --download-metadata --newest-only -p=/mnt/
```

### doceker save (docker image -> tar)
Before do it you must pull image what you want to save image

```
docker save -o nginx.tar nginx.latest
```

### docker load (tar -> docker image)

```
docker load -i nginx.tar
```

## Ubuntu repo 설정


```

```



