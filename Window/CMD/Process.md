# 프로세스 관련 명령어


필요한 서비스 확인

```cmd
tasklist | findstr "ecl"
```

![image](https://user-images.githubusercontent.com/38831314/123749355-4cf7f000-d8f0-11eb-805f-9b4dc126e495.png)

Kill 명령어는 해당 PID 활용

```cmd
taskkill /f /pid 18468
```

![image](https://user-images.githubusercontent.com/38831314/123749517-7ca6f800-d8f0-11eb-9a82-dc63bfea0b69.png)
