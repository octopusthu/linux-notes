# System

## Initial Setup

### Must-Install Packages and Software

- zsh

```bash
sudo apt install zsh

chsh
/bin/zsh
```

- oh-my-zsh

[Install Oh My Zsh](https://ohmyz.sh/)

- git

```bash
git config --global credential.helper 'store'
git config --global user.name "octopusthu"
git config --global user.email octopusthu@gmail.com
```

### Set Timezone

```bash
mv /etc/localtime /etc/localtime.backup
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

## SSH

- Basic config

```bash
vim /etc/ssh/sshd_config
    Port xxxxx
    PasswordAuthentication no
systemctl restart sshd
```

- Login using a non-root user with an RSA key via a customized port

client

```bash
ssh-keygen -t rsa
```

server

```bash
su - zy
mkdir ~/.ssh
vim ~/.ssh/authorized_keys
    pub key content
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
vim /etc/ssh/sshd_config
    Port xxxxx
    PasswordAuthentication no
    PermitRootLogin no
systemctl restart sshd
```

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

## firewalld

- /usr/lib/firewalld/services
- /etc/firewalld/services

```bash
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --info-service=http
firewall-cmd --reload

firewall-cmd --get-active-zones
firewall-cmd --list-all-zones
firewall-cmd --zone=public --list-all

firewall-cmd --zone=public --add-port=12345/tcp
firewall-cmd --zone=public --remove-port=12345/tcp
```

## Yum

- [IUS Community Project](https://ius.io/)

## Misc

- Warning upon login: `-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory`

```bash
vi /etc/environment

# add these lines...

LANG=en_US.utf-8
LC_ALL=en_US.utf-8
```
