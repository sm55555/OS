# how to install speccifci package

### 1. first remove all relative package

```
[root@test_d ~]# yum --showduplicate list [package_name]

[root@test_d ~]# yum --showduplicate list firefox
Loaded plugins: langpacks, product-id, search-disabled-repos, subscription-manager
This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.
Repodata is over 2 weeks old. Install yum-cron? Or run: yum makecache fast
Available Packages
firefox.x86_64                                                              24.5.0-1.el7                                                                RHEL7
firefox.x86_64                                                              24.6.0-1.el7_0                                                              RHEL7
firefox.x86_64                                                              24.7.0-1.el7_0                                                              RHEL7
firefox.x86_64                                                              24.8.0-1.el7_0                                                              RHEL7
firefox.x86_64                                                              31.1.0-6.el7_0                                                              RHEL7
firefox.x86_64                                                              31.2.0-3.el7_0                                                              RHEL7
firefox.x86_64                                                              31.3.0-3.el7_0                                                              RHEL7
firefox.x86_64                                                              31.4.0-1.el7_0                                                              RHEL7
firefox.x86_64                                                              31.5.0-2.el7_0                                                              RHEL7
firefox.x86_64                                                              31.5.3-3.el7_1                                                              RHEL7
firefox.x86_64                                                              31.6.0-2.el7_1                                                              RHEL7
firefox.x86_64                                                              38.0-3.el7_1                                                                RHEL7
firefox.x86_64                                                              38.0.1-1.el7_1     


[root@test_d ~]# yum install [package-name]-[version].[architecture]   -> ex) yum install httpd-2.4.43-1.amzn2

```

source url : https://www.thegeekdiary.com/centos-rhel-how-to-install-a-specific-version-of-rpm-package-using-yum/


### 2. checked Available Packages Version

```

[root@test_d ~]# yum info httpd
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
202 packages excluded due to repository priority protections
Installed Packages
Name        : httpd
Arch        : x86_64
Version     : 2.4.43
Release     : 1.amzn2
Size        : 4.0 M
Repo        : installed
From repo   : amzn2-core
Summary     : Apache HTTP Server
URL         : https://httpd.apache.org/
License     : ASL 2.0
Description : The Apache HTTP Server is a powerful, efficient, and extensible
            : web server.

Available Packages
Name        : httpd
Arch        : x86_64
Version     : 2.4.46
Release     : 1.amzn2
Size        : 1.3 M
Repo        : amzn2-core/2/x86_64
Summary     : Apache HTTP Server
URL         : https://httpd.apache.org/
License     : ASL 2.0
Description : The Apache HTTP Server is a powerful, efficient, and extensible
            : web server.



```

### if you can't see Available Packages~~~

```
[root@test_d ~]# yum install -y epel-release
[root@test_d ~]# cd /etc/yum.repos.d && wget https://repo.codeit.guru/codeit.el`rpm -q --qf "%{VERSION}" $(rpm -q --whatprovides redhat-release)`.repo
[root@test_d ~]# yum info httpd
```

source url : https://okcn.tistory.com/356
