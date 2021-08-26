# Powershell Command

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


