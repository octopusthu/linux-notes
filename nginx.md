### Installation
- [nginx: Linux packages](https://nginx.org/en/linux_packages.html)
  ```bash
  vim /etc/yum.repos.d/nginx.repo
  
  [nginx]
  name=nginx repo
  baseurl=http://nginx.org/packages/centos/7/$basearch/
  gpgcheck=0
  enabled=1
  
  yum install nginx
  ``` 

### Config

### Logs
- /var/log/nginx/

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

