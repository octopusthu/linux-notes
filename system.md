# System

## Kernel

- [How to Install or Upgrade to Kernel 4.14 in CentOS 7](https://www.tecmint.com/install-upgrade-kernel-version-in-centos-7/)

- [How to Deploy Google BBR on CentOS 7](https://www.vultr.com/docs/how-to-deploy-google-bbr-on-centos-7)

## Service Management

```bash
systemctl status shadowsocks
systemctl list-unit-files | grep php-fpm
systemctl list-unit-files | grep enabled
```

## Users & Groups

```bash
useradd zy && passwd zy
groupadd ${newGroup}
groups zy
usermod -aG wheel zy
gpasswd -d ${user} ${group}
```

## Monitoring

```bash
aureport -au --success
aureport -au --failed
aureport -l --success
aureport -l --failed

last root
lastb -10
```

## Environment variables

- /etc/profile.d/*.sh

```sh
JAVA_HOME=/usr/java/default
PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME
```

## Misc
