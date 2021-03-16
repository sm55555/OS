### 몇일 이상 된 파일 지우기

30일 이상된 파일 출력

find /logs/*.log.* -ctime +30


30일 이상된 파일 지우는 스크립트

```
#!/bin/bash
cd /logs
find ./*.log.* -ctime +30 -exec rm -f {} \;
```

### 특정 로그를 지우고 삭제 전과 동일한 용량을 보일때
 
lsof | grep deleted

<img src="https://user-images.githubusercontent.com/38831314/111253864-39818b80-8657-11eb-83d6-6ef63711c8be.png">

출력된 결과에서 아까 삭제했던 파일을 찾아서 어떤 프로세스에서 아직 파일을 사용 중인지 확인할 수 있다. 
