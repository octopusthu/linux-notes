# V2Ray
### Server
- Install/Upgrade
```
su
bash <(curl -L -s https://install.direct/go.sh)
```
- config
```
vim /etc/v2ray/config.json
```
- log
```
tail -f /var/log/v2ray/error.log
tail -f /var/log/v2ray/access.log
```
### Client
- Install/Upgrade
  1. [Download](https://github.com/v2ray/v2ray-core/releases)
  2. Install
    - ~/Documents/apps/v2ray/
  3. Restart
  ```
  kill -1 $pid
  or
  supervisorctl restart v2ray
  ```
- config
  - ~/Documents/config/v2ray/config.json
- log
```
tail -f ~/Documents/config/v2ray/error.log
tail -f ~/Documents/config/v2ray/access.log
```

### Local - Relay - Server
- Local
- Relay
- Server