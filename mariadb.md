# Installation
- Download and Install
```bash
sudo /etc/yum.repos.d/MariaDB.repo
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.2/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1

sudo yum install MariaDB-server

sudo systemctl enable mariadb
sudo systemctl start mariadb
```

- Secure the MariaDB Server
```bash
sudo mysql_secure_installation
```

- Config
```bash
sudo vim /etc/my.cnf.d/server.cnf
[mysqld]
port=${port}

sudo systemctl restart mariadb
```

- Grants
```bash
mysql -u root -p

CREATE USER 'zy'@'localhost' IDENTIFIED BY '1';
grant all privileges on *.* to 'zy'@'%' with grant option;
flush privileges;
```
