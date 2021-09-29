# AD 관련 명령어

### Number of User Accounts

(get-aduser -filter *).count

### Number of Enabled User Accounts

(get-aduser -filter *|where {$_.enabled -eq “True”}).count

### Number of Disabled User Accounts

(get-aduser -filter *|where {$_.enabled -ne “False”}).count

### Number of Enabled User Accounts in Sepcific OU

(get-aduser -filter * -SearchBase “OU=Division,DC=test,DC=com” |where {$_.enabled -eq “True”}).count

### Account information

Get-ADUser –Identity “delmaster” –Properties *

### 최근 몇일내 생성된 계정 조회

$Days = 1
$Time = (Get-Date).Adddays(-($Days))
Get-ADUser -Filter * -Property whenCreated | Where {$_.whenCreated -gt $Time} | ft Name, WhenCreated

### 특정 계정 그룹 넣기

Add-ADGroupMember -Identity [그룹이름] -Member [사용자 이름]

## 특정 계정의 소속 그룹 정보

Get-ADPrincipalGroupMembership [사용자 이름] | select name
