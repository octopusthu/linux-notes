### Installation

```bash
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --zone=public --add-service=https--permanent
firewall-cmd --reload
```

### HTTPS

```bash
yum install certbot
certbot certonly --webroot -w /usr/share/nginx/html/ -d octopusthu.com -d www.octopusthu.com
```
