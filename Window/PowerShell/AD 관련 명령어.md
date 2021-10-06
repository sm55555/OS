# AD 관련 명령어

### Number of User Accounts

```powershell
(get-aduser -filter *).count
```

### Number of Enabled User Accounts

```powershell
(get-aduser -filter *|where {$_.enabled -eq “True”}).count
```

### Number of Disabled User Accounts

```powershell
(get-aduser -filter *|where {$_.enabled -ne “False”}).count
```

### Number of Enabled User Accounts in Sepcific OU
```powershell
(get-aduser -filter * -SearchBase “OU=Division,DC=test,DC=com” |where {$_.enabled -eq “True”}).count

만약 co.kr 로 끝나면 아래와 같이 수정

(get-aduser -filter * -SearchBase “OU=Division,DC=test,DC=co,DC=kr” |where {$_.enabled -eq “True”}).count
```

### Account information

delmaster 사용자 정보 조회

```powershell
Get-ADUser –Identity “delmaster” –Properties *
```

### 최근 몇일내 생성된 계정 조회

$Days 값으로 지정한다.

```powershell
$Days = 1
$Time = (Get-Date).Adddays(-($Days))
Get-ADUser -Filter * -Property whenCreated | Where {$_.whenCreated -gt $Time} | ft Name, WhenCreated
```

### 특정 계정 그룹 넣기

```powershell
Add-ADGroupMember -Identity [그룹이름] -Member [사용자 이름]
```

### 특정 계정의 소속 그룹 정보

```powershell
Get-ADPrincipalGroupMembership [사용자 이름] | select name
```

### 특정 OU, 특정 기간내 생성된 계정 정보

$Days 값으로 지정한다.

```powershell
$Days = 1
$Time = (Get-Date).Adddays(-($Days))
get-aduser -filter * -SearchBase “OU=testuser,DC=hist,DC=co,DC=kr” -Property whenCreated | Where {$_.whenCreated -gt $Time} | ft Name, WhenCreated
```

### 특정 OU 사용자들의 특정 정보 추출

```powershell
Get-ADUser -Filter * -SearchBase “OU=하위OU,OU=상위OU,DC=test,DC=co,DC=kr” -Property * | ft MemberOf
```

### 엄청 긴거 출력할 때

Format-Table -Wrap -AutoSize 옵션 추가
Out-File -Width 2500 이걸 추가해야 길게 늘어져서 ... 안보임
-FilePath d:\test.txt 파일 저장할 방식

```powershell
Get-ADUser -Filter * -SearchBase “OU=ITRO,OU=DIVISION,DC=kalmate,DC=net” -Property * | Format-Table -Wrap -AutoSize Name, Description, title, EmailAddress, mail, EMailExternal, UserPrincipalName, CN, GivenName, sn, DisplayName, MemberOf, unicodePwd, ObjectGUID, CanonicalName, displayNamePrintable, DistinguishedName, extensionAttribute7, mailNickname, SamAccountName, targetAddress | Out-File -Width 2500 -FilePath d:\test.txt
```

