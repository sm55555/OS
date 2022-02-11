### 1. ROOT 계정으로 전환(원활한 작업을 위해)

```
[user@localhost ~]$ su - 
Password: 
Last login: Mon Jan 11 00:25:59 EST 2021 on pts/2
```
 

### 2. 현재 자바버전 확인

```
[root@localhost ~]# java -version
Java version "1.6.0_43"
Java(TM) SE Runtime Environment (build 1.6.0_43-b01)
Java HotSpot(TM) 64-bit Server VM (build 20.14-b01, mixed mode)
``` 
 
### 3. 설치 가능한 openJDK버전 확인

```
[root@localhost ~]# yum list java*jdk-devel
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.kakao.com
 * extras: mirror.kakao.com
 * updates: mirror.kakao.com
Available Packages
java-1.6.0-openjdk-devel.x86_64         1:1.6.0.41-1.13.13.1.el7_3        base    
java-1.7.0-openjdk-devel.x86_64         1:1.7.0.261-2.6.22.2.el7_8        base    
java-1.8.0-openjdk-devel.i686           1:1.8.0.275.b01-0.el7_9           base
java-1.8.0-openjdk-devel.x86_64         1:1.8.0.275.b01-0.el7_9           base
java-11-openjdk-devel.i686              1:11.0.9.11-2.el7_9               updates 
java-11-openjdk-devel.x86_64            1:11.0.9.11-2.el7_9               updates 
```

### 4. 원하는 버전 다운로드

```
[root@localhost ~]# yum install -y java-1.8.0-openjdk-devel.i686
Installing : ...
Updating : ...
...
Installed:
  java-1.8.0-openjdk-devel.i686 1:1.8.0.275.b01-0.el7_9  
...
Complete!
``` 

### 5. Alternatives로 Default Java 변경하기 (버전이 변경되지 않았을 경우)

```
[root@localhost ~]# java -version
Java version "1.6.0_43"
Java(TM) SE Runtime Environment (build 1.6.0_43-b01)
Java HotSpot(TM) 64-bit Server VM (build 20.14-b01, mixed mode)

[root@localhost ~]# /usr/sbin/alternatives --config java

There are 1 programs which provide 'java'.

  Selection    Command
-----------------------------------------------
+ 1           java-1.8.0-openjdk.i386 (/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.275.b01-0.el7_9.i386/jre/bin/java)

Enter to keep the current selection[+], or type selection number: 1
``` 

### 6. 환경변수 재지정하기

: 나의 경우 위 5번을 진행해도 여전히 1.6버전임을 확인할 수 있었는데, 이는 리눅스 환경변수로 1.6 버전이 지정되어 있기 때문이었다. 때문에 환경변수도 함께 변경을 진행한다.


```
[root@localhost ~]# echo $JAVA_HOME
/usr/local/java/jdk1.6.0_43
[root@localhost ~]# echo $PATH
/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/java/jdk1.6.0_43/bin:/root/bin
[root@localhost ~]# vi /etc/profile

# /etc/profile

# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc

...

JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.275.b01-0.el7_9.i386
export JAVA_HOME
PATH=$PATH:$JAVA_HOME/bin
export PATH

...
```


### 7. 자바 버전 확인

```
[root@localhost ~]# java -version
openjdk version "1.8.0_275"
OpenJDK Runtime Environment (build 1.8.0_275-b01)
OpenJDK Server VM (build 25.275-b01, mixed mode)
```
