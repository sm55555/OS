### 끝판 왕 명령어

<span style="color: red;">This text is red.</span>


```sh
#!/bin/bash

# Define the path to the directory
folderPath="/path/to/your/directory"

# Find and delete files older than 5 days
find "$folderPath" -type f -mtime +5 -exec rm -f {} \;

# Find and delete empty directories
find "$folderPath" -type d -empty -delete
```

### 몇일 이상 된 폴더 지우기

30일 이상된 폴더 출력

```sh
#!/bin/bash
find /logs -type -d -ctime +30
```


### 몇일 이상 된 파일 지우기

30일 이상된 파일 출력

```sh
find /logs/*.log.* -ctime +30
```

30일 이상된 파일 지우는 스크립트

```sh
#!/bin/bash
find /logs/*.log.* -ctime +30 -exec rm -f {} \;
```

### 특정 로그를 지우고 삭제 전과 동일한 용량을 보일때
 
프로세스에서 삭제된 파일들을 사용하는 경우가 있다.

``` sh
lsof | grep deleted
```

명령어를 동해서 현재 사용하고 있는 프로세스를 확인한다.

<img src="https://user-images.githubusercontent.com/38831314/111253864-39818b80-8657-11eb-83d6-6ef63711c8be.png">

출력된 결과에서 아까 삭제했던 파일을 찾아서 어떤 프로세스에서 아직 파일을 사용 중인지 확인할 수 있다. 

### 파일 내용 없애기

messages 용량이 너무 많은 경우

```
cat  /dev/null > messages
```
