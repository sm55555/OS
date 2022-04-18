## Path 적용

예를 들어서 PHP에 대한 명령어가 /usr/local/php/bin 하위에 있다고 하자. 그럼 PATH 환경 변수에 추가해야한다.

```
vi ~/.bashrc
export PATH=:"........:/usr/local/php/bin"
```

추가한 다음

```
source ~/.bashrc
```

적용

### 결과 확인

```
php -v
php -m
```
