#### 1. Repo 서버에 웹서버 nginx 를 설치

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
rsync -avrt --progress rsync://mirror.centos.org/ /data/rocky/
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
curl -v http://mirror.centos.org/centos/baseos/repodata/repomd.xml
curl -v http://dl.rockylinux.org/rocky/baseos/repodata/repomd.xml
```


### 도커 올리고하는방법

baseos, appstream, extras, epel

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

```
createrepo /mnt/appstream
```

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

nginx가 있다는 가정하에 현재는 조회하면 /data 하위에 바라보게 되어 있다. centos, rocky 나누어져 있기 떄문

```
sudo cp /usr/bin/apt-mirror /usr/bin/apt-mirror.original
sudo chown root:root /usr/bin/apt-mirror && sudo chmod 755 /usr/bin/apt-mirror
```

/etc/apt/mirror.list

```
############# config ##################
#
# set base_path    /var/spool/apt-mirror
#
# set mirror_path  $base_path/mirror
# set skel_path    $base_path/skel
# set var_path     $base_path/var
# set cleanscript $var_path/clean.sh
# set defaultarch  <running host architecture>
# set postmirror_script $var_path/postmirror.sh
# set run_postmirror 0
set nthreads     20
set _tilde 0
#
############# end config ##############
 
deb http://kr.archive.ubuntu.com/ubuntu focal main restricted
deb http://kr.archive.ubuntu.com/ubuntu focal-updates main restricted
deb http://kr.archive.ubuntu.com/ubuntu focal universe
deb http://kr.archive.ubuntu.com/ubuntu focal-updates universe
deb http://kr.archive.ubuntu.com/ubuntu focal multiverse
deb http://kr.archive.ubuntu.com/ubuntu focal-updates multiverse
deb http://kr.archive.ubuntu.com/ubuntu focal-backports main restricted universe multiverse
deb http://kr.archive.ubuntu.com/ubuntu focal-security main restricted
deb http://kr.archive.ubuntu.com/ubuntu focal-security universe
deb http://kr.archive.ubuntu.com/ubuntu focal-security multiverse
```

대략 250GB 정도된다.

```
apt-mirror

심볼릭 링크 변경

ln -s /var/spool/apt-mirror/mirror/kr.archive.ubuntu.com/ubuntu/ /data
```

client 설정 /etc/hosts
```
111.222.333.444 archive.ubuntu.com

yum install chrony

```


