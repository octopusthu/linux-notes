### Installation

```bash
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --zone=public --add-service=https--permanent
firewall-cmd --reload
```

### HTTPS
- /etc/nginx/conf.d/ssl.conf
- /etc/nginx/default.d/ssl-redirect.conf
