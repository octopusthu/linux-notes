
### Users & Groups
```bash
useradd ${user} && passwd ${user}

usermod -aG wheel ${user}

gpasswd -d ${user} ${group}
```

### SSH
- ~/.ssh/sshd_config
	- PasswordAuthentication no
	- PermitRootLogin no
	
- ~/.ssh/authorized_keys

```bash
sudo chmod 700 -R ~/.ssh && chmod 600 ~/.ssh/authorized_keys
```

### firewalld

##### services
- /usr/lib/firewalld/services
- /etc/firewalld/services

```bash
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --reload

firewall-cmd --get-active-zones
firewall-cmd --list-all-zones
firewall-cmd --zone=public --list-all

firewall-cmd --zone=public --add-port=12345/tcp
firewall-cmd --zone=public --remove-port=12345/tcp
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

### vsftpd
- /etc/vsftpd/vsftpd.conf
```
pasv_enable=Yes
pasv_max_port=10100
pasv_min_port=10090
```
- firewalld
```bash
firewall-cmd --permanent --zone=public --add-port=10090-10100/tcp
```
- trim trailing spaces 
```bash
sed -i 's,\r,,;s, *$,,' /etc/vsftpd.conf
```
- TLS
	- [How To Configure vsftpd to Use SSL/TLS on a CentOS VPS](https://www.digitalocean.com/community/tutorials/how-to-configure-vsftpd-to-use-ssl-tls-on-a-centos-vps)

### Services
```bash
systemctl list-unit-files | grep php-fpm
systemctl list-unit-files | grep enabled
```

### yum


