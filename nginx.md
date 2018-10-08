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

##### Configure Nginx and Certbot 

- Configure Nginx
  - /etc/nginx/conf.d/ssl.conf
  - /etc/nginx/default.d/ssl-redirect.conf

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

##### Configure Certbot the automatic way
- [certbot](https://certbot.eff.org/lets-encrypt/centosrhel7-nginx)
  - pkg_resources.DistributionNotFound: The 'PyOpenSSL>=0.13' distribution was not found and is required by josepy, acme
    ```bash
    sudo yum reinstall pyOpenSSL
    ```
  - pkg_resources.DistributionNotFound: The 'idna>=2.1' distribution was not found and is required by cryptography
  ```bash
    sudo yum reinstall python-idna
    ```

