## PHP 관련 명렁어 안될때

### Check PHP Installation in Rocky Linux

```
$ php -v
-bash: php: command not found
```

### Install PHP 7.2 in Rocky Linux

```
$ sudo dnf module list php 
$ sudo dnf module enable php:7.2
$ sudo dnf module enable php:7.2
$ sudo dnf install php php-cli php-gd php-curl php-zip php-mbstring
```
### Verify the Version of PHP Installed

```
$ php -v
```

참고 
https://www.tecmint.com/install-php-7-on-rocky-linux/
