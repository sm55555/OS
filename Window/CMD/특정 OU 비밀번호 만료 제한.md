### 특정 OU 비밀번호 만료 제한

그룹 정책보다 우선인 [속성]으로 비밀번호 만료 제한

아래 그림처럼 일일이 선택하는거 명령어로 대체

![image](https://user-images.githubusercontent.com/38831314/135550843-6f0fc46f-18f2-4f35-a470-6a59dcdf1aeb.png)

#### 100명 이하

```cmd
dsquery user OU=관리,DC=test,DC=co,DC=kr | dsmod user -pwdneverexpires yes
```

#### 100명이 넘는 경우

```cmd
dsquery user -limit 1000 OU=관리,DC=test,DC=co,DC=kr | dsmod user -pwdneverexpires yes
```
