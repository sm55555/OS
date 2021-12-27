## 위치 매개변수

- 입력하는 argument들은 $0, $1, $2와 같은 변수에 저장되어 script에 전달

```
name of shell script : $0
first argument : $1
second argument : $2
Number of arguments : $#
List of parameters : $@, $*
```

- Special shell variables

로그인 shell의 PID : $$
현재 작업 디렉토리 : $PWD
부모 프로세스 ID : $PPID


### ex) parameter.sh red blue

```
#!/bin/bash
echo "first $0"
echo "second $1"
echo "third $2"

--- 결과 ---

first parameter.sh
red
blue
```
