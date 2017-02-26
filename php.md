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

- /etc/nginx/conf.d/ssl.conf
```
server {
	...
	index       index.php index.html index.htm;
	location / {
		try_files $uri $uri/ =404;
	}
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
	
	...
}
```

- session folder permission
```bash
chmod -R 777 /var/lib/php/session
```