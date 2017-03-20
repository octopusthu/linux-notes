### Installation
- rpm
```bash
rpm -ivh jdk-8u121-linux-x64.rpm
```

- env
```bash
vi /etc/profile.d/java.sh
```

```
JAVA_HOME=/usr/java/default
PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME
```

```bash
chmod +x java.sh
source java.sh
```

### Config

