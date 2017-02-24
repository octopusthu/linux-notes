### Config

- /etc/php.ini
```
cgi.fix_pathinfo=0
```

- /etc/php-fpm.d/www.conf
```
listen=/var/run/php-fpm/php-fpm.sock
listen.owner=nobody
listen.group=nobody
user=nginx
group=nginx
```