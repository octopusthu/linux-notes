# Misc

## Supervisor

- Installing

```bash
easy_install supervisor
echo_supervisord_conf
echo_supervisord_conf > /etc/supervisord.conf
```

- Run on startup

```bash
cd /etc/systemd/system
wget https://raw.githubusercontent.com/Supervisor/initscripts/master/centos-systemd-etcs
mv centos-systemd-etcs supervisord.service
systemctl start supervisord
systemctl enable supervisord
```

- Logging

```bash
tail -f /tmp/supervisord.log
```

- Add a program

```bash
vim /etc/supervisord.conf

[program:shadowsocksr]
command=python server.py -c ../user-config.json  ; the program (relative uses PATH, can take args)
directory=/etc/shadowsocksr/shadowsocks  ; directory to cwd to before exec (def no cwd)
stdout_logfile=/etc/shadowsocksr/supervisor.log  ; stdout log path, NONE for none; default AUTO

kill -1 $pid
```

- Status

```bash
supervisorctl status
```
