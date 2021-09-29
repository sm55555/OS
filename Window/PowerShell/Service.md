# 서비스 관련 파워쉘 명령어


### 서비스 조회

```cmd
powershell Get-Service [서비스 명]
```

### 서비스 종료

```cmd
powershell Stop-Service [서비스 명] -Force
```

### 서비스 사용안함

```powershell
powershell Set-Service [서비스 명] -StartupType Disabled
```

