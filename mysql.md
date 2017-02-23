### Installation
- MySQL v 5.7 or higher generates a temporary random password after installation
```bash
grep 'temporary password' /var/log/mysqld.log
```

- Security steps
```bash
mysql_secure_installation
```

### Config
- /etc/my.cnf
```
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

### Grants
```bash
grant all on testdb.* to 'zhangyu'@'%' identified by '${password}';

grant all privileges on *.* to 'zhangyu'@'%' identified by '${password}';
```

### phpMyAdmin
```bash

```