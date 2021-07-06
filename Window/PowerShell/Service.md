# 서비스 관련 파워쉘 명령어


### 서비스 조회

```cmd
powershell Get-Service Spooler
```

### 서비스 종료

```cmd
powershell Stop-Service Spooler -Force
```

### 서비스 사용안함

```cmd
powershell Set-Service Spooler -StartupType Disabled
```

