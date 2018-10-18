### Kernel
- [How to Install or Upgrade to Kernel 4.14 in CentOS 7](https://www.tecmint.com/install-upgrade-kernel-version-in-centos-7/)
- [How to Deploy Google BBR on CentOS 7](https://www.vultr.com/docs/how-to-deploy-google-bbr-on-centos-7)

### Service Management
```bash
systemctl status shadowsocks
systemctl list-unit-files | grep php-fpm
systemctl list-unit-files | grep enabled
```

### Users & Groups
```bash
useradd zy && passwd zy
groupadd ${newGroup}
groups zy
usermod -aG wheel zy
gpasswd -d ${user} ${group}
```

### SSH
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

### Supervisor
- Installing
```bash
easy_install supervisor
echo_supervisord_conf
echo_supervisord_conf > /etc/supervisord.conf
```
- Run on startup
```bash
cd /etc/systemd/system
wget https://raw.githubusercontent.com/Supervisor/initscripts/master/centos-systemd-etcs
mv centos-systemd-etcs supervisord.service
systemctl start supervisord
systemctl enable supervisord
```

- Logging
```bash
tail -f /tmp/supervisord.log
```

- Add a program
```bash
vim /etc/supervisord.conf

[program:shadowsocksr]
command=python server.py -c ../user-config.json  ; the program (relative uses PATH, can take args)
directory=/etc/shadowsocksr/shadowsocks  ; directory to cwd to before exec (def no cwd)
stdout_logfile=/etc/shadowsocksr/supervisor.log  ; stdout log path, NONE for none; default AUTO

kill -1 $pid
```

- Status
```bash
supervisorctl status
```

### Monitoring

```bash
aureport -au --success
aureport -au --failed
aureport -l --success
aureport -l --failed

last root
lastb -10
```


### Environment variables
- /etc/profile.d/*.sh
```
JAVA_HOME=/usr/java/default
PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME
```

### firewalld

##### services
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

### Yum
- [IUS Community Project](https://ius.io/)
