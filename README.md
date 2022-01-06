# linux-notes

Notes and tips in regard to Linux installation, configuration and maintenance.

## Current OS

- Ubuntu 20.04 LTS
- Ubuntu 21.10

## History OS

- CentOS 7
- CentOS 8

## Must-Install Packages

### zsh

- Install Zsh

```bash
sudo apt install zsh

chsh
/bin/zsh
```

- [Install Oh My Zsh](https://ohmyz.sh/)
- Use oh-my-zsh Gitee Mirror

```bash
wget https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh
REMOTE=https://gitee.com/mirrors/oh-my-zsh.git BRANCH=master sh install.sh
```

- Edit `~/.zshrc` to enable common plugins (such as docker) and include any startup scripts

### Docker

- [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
  - Use a [mirror](https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/)
  - After installation, edit `/etc/docker/daemon.json` to use a Docker Registry Mirror, which is usually vendor-specific, such as `https://mirror.ccs.tencentyun.com` provided by Tencent Cloud.

- [Post-installation steps for Linux](https://docs.docker.com/engine/install/linux-postinstall/), e.g., run docker commands as a non-root user

- [Install Docker Compose V2 on Linux](https://docs.docker.com/compose/cli-command/#install-on-linux)

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

- Set hostname (For packages like `sendmail` to function)
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
