# 참고 

https://superuser.com/questions/1386209/how-to-solve-this-dependencies-apt-fix-broken-install


```
Reading package lists... Done
Building dependency tree
Reading state information... Done
Correcting dependencies... failed.
The following packages have unmet dependencies:
libhogweed4 : Depends: libnettle6 (= 3.3-1+b1) but 3.4-1 is installed
mana-toolkit : Depends: dnsmasq but it is not installable
E: Error, pkgProblemResolver::Resolve generated breaks, this may be caused by held packages.
E: Unable to correct dependencies
```

조치방법

```
dpkg --force-all --configure -a
dpkg --purge --force-depends libnettle6 (cf. this post)
apt --fix-broken install
apt-get -f install
```
