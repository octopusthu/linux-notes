### Installation

```bash
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --zone=public --add-service=https--permanent
firewall-cmd --reload
```

### HTTPS
- /etc/nginx/conf.d/ssl.conf
- /etc/nginx/default.d/ssl-redirect.conf


### Certificates
- Create a certificate
```bash
yum install certbot
certbot certonly --webroot -w /usr/share/nginx/html/ -d octopusthu.com -d www.octopusthu.com
```

- Automatic renewal
	- /etc/systemd/system/certbot-renew.service
	- /etc/systemd/system/certbot-renew.timer
	
```bash
systemctl start certbot-renew.timer
systemctl enable certbot-renew.timer
```

