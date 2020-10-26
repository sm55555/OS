### how to install speccifci package

first remove all relative package

```

# yum --showduplicate list [package_name]


# yum --showduplicate list firefox
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


# yum install [package-name]-[version].[architecture]   -> ex) yum install httpd-2.4.43-1.amzn2




```
