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
