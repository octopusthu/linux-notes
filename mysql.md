# MySQL

## Installation

- MySQL v 5.7 or higher generates a temporary random password after installation

  ```bash
  grep 'temporary password' /var/log/mysqld.log
  ```

- Security steps

  ```bash
  mysql_secure_installation
  ```

## Config

- /etc/my.cnf

  ```mysql
  [mysqld]
  port=${port}
  [client]
  port=${port}
  ```

- Firewall

  ```bash
  firewall-cmd --zone=public --add-rich-rule 'rule family="ipv4" source address="x.x.0.0/16" port port=${port} protocol=tcp accept' --permanent
  firewall-cmd --reload
  ```

## Grants

```bash
CREATE USER 'zhangyu'@'localhost' IDENTIFIED BY '1';
grant all on testdb.* to 'zhangyu'@'%';
grant all privileges on *.* to 'zhangyu'@'%' with grant option;
flush privileges;
```

## phpMyAdmin

```bash
yum install php-mysql php-fpm
```

```bash
ln -s /usr/share/phpMyAdmin /usr/share/nginx/html
mv /usr/share/nginx/html/phpMyAdmin /usr/share/nginx/html/pma
systemctl restart php-fpm
```

- /etc/phpMyAdmin/config.inc.php

  ```php
  $cfg['Servers'][$i]['host']    = '127.0.0.1';
  $cfg['Servers'][$i]['port']    = '15906';
  ```
