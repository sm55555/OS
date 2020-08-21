### java install

github.com/ojdkbuild/contrib_jdk8u-ci/releases

해당 버전 받고 압축 푼거 /etc/profile 아래에 추가

export JAVA_HOME=/usr/java/jdk-8u242-ojdkbuild-linux-x64
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH="." 

source /etc/profile

java -version 확인

### nginx install

blog.dalso.org/uncategorized/2072
nginx.org/en/download.html
wget으로 필요한 버전 받고

yum install gcc
yum install gcc-c++
yum install pcre-devel
yum groupinstall "Development tools"
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel

nginx 폴더에서 ./configure 실행 성공 후 -> make && install 후 성공

시작 명령어
cd /usr/local/nginx/sbin/
./nginx 실행

중지 명령어 ./nginx -s stop

버전 확인 명령어 curl -I localhost

### tomcat install

archive.apache.org/dist/tomcat/

에 가서 받는다.

필요한게 있으면 conf /server.xml 에서 포트 변경

### jenkins install

$ sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

-jenkins 저장소 키 등록
$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

$ sudo yum install jenkins

$ sudo service jenkins start

여기서 안되면 젠킨스 스크립트 자바 주소 추가 해줘야한다 .

젠킨스 스크립트 위치 /etc/rc.d/init.d/ -> vi jenkins   -> java 주소 적혀있는데 넣어주자,.

 자바 주소 확인은 which java

5. EC2에서 8080 포트 열고 http://aws-ec2-domain:8080으로 접속

7. 사이트에서 가르키는 경로에서 비밀번호를 확인 후, 플러그인(suggest)설치



