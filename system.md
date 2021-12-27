# System

## Must-Install Packages

- zsh

```bash
sudo apt install zsh

chsh
/bin/zsh
```

- oh-my-zsh

[Install Oh My Zsh](https://ohmyz.sh/)

## Configurations

- Configure Git

```bash
git config --global credential.helper 'store'
git config --global user.name "octopusthu"
git config --global user.email octopusthu@gmail.com
```

- Set timezone

```bash
mv /etc/localtime /etc/localtime.backup
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# Change to 24hr format (need re-login)
localectl set-locale LC_TIME=en_GB.UTF-8
```

- Set hostname (For packages like `sendmail` to function normal)
  - `hostnamectl set-hostname example.com`
  - In /etc/hosts, assign the just updated hostname `example.com` to `127.0.0.1`

## SSH

- Basic config

```bash
sudo vim /etc/ssh/sshd_config
    Port xxxxx
    PasswordAuthentication no
sudo systemctl restart sshd
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

## Unattended Upgrades

- [UnattendedUpgrades](https://wiki.debian.org/UnattendedUpgrades)
  - Need the `sendmail` package to send notifications via email

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
