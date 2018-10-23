# Misc

### V2Ray
##### Server
- Install/Upgrade
```
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
##### Client
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

##### Local - Relay - Server
Replace ${...} with proper values.
- Local
```json
{
  "log": {
    "access": "${v2ray}/access.log",
    "error": "${v2ray}/error.log",
    "loglevel": "warning"
  },
  "routing": {
    "strategy": "rules",
    "settings": {
      "rules": [
        {
          "type": "field",
          "inboundTag": ["relay"],
          "outboundTag": "relay"
        }
      ]
    }
  },
  "inbound": {
    "port": 65530,
    "listen": "127.0.0.1",
    "protocol": "shadowsocks",
    "settings": {
      "email": "local",
      "method": "aes-128-cfb",
      "password": "1",
      "udp": false,
      "level": 1,
      "ota": false
    }
  },
  "inboundDetour": [
    {
      "tag": "relay",
      "port": 65531,
      "listen": "127.0.0.1",
      "protocol": "shadowsocks",
      "settings": {
        "email": "local",
        "method": "aes-128-cfb",
        "password": "1",
        "udp": false,
        "level": 1,
        "ota": false
      }
    }
  ],
  "outbound": {
    "protocol": "vmess",
    "settings": {
      "vnext": [
        {
          "address": "${server-address}",
          "port": 65532,
          "users": [
            {
              "id": "${server-password}"
            }
          ]
        }
      ]
    },
    "streamSettings": {
      "network": "tcp",
      "security": "tls",
      "tlsSettings": {
        "allowInsecure": true
      }
    },
    "mux": {
      "enabled": true,
      "concurrency": 8
    }
  },
  "outboundDetour": [
    {
      "tag": "relay",
      "protocol": "socks",
      "settings": {
        "servers": [
          {
            "address": "${relay-address}",
            "port": 65532,
            "users": [
              {
                "user": "${relay-user}",
                "pass": "${relay-password}"
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "tcp",
        "security": "tls",
        "tlsSettings": {
          "allowInsecure": true
        }
      },
      "mux": {
        "enabled": true,
        "concurrency": 8
      }
    }
  ],
  "policy": {
    "levels": {
      "0": {
        "uplinkOnly": 0
      }
    }
  }
}
```

- Relay
```json
{
  "log": {
    "access": "/var/log/v2ray/access.log",
    "error": "/var/log/v2ray/error.log",
    "loglevel": "warning"
  },
  "inbound": {
    "port": 65532,
    "protocol": "socks",
    "settings": {
      "auth": "password",
      "accounts": [
        {
          "user": "${relay-user}",
          "pass": "${relay-password}"
        }
      ],
      "udp": true,
      "ip": "127.0.0.1",
      "timeout": 30,
      "userLevel": 0
    },
    "streamSettings": {
      "network": "tcp",
      "security": "tls",
      "tlsSettings": {
        "certificates": [
          {
            "certificate": [
              "-----BEGIN CERTIFICATE-----",
              "${certificate-content...}",
              "-----END CERTIFICATE-----"
            ],
            "key": [
              "-----BEGIN RSA PRIVATE KEY-----",
              "${key-content...}",
              "-----END RSA PRIVATE KEY-----"
            ]
          }
        ]
      }
    }
  },
  "outbound": {
    "protocol": "vmess",
    "settings": {
      "vnext": [
        {
          "address": "${server-address}",
          "port": 65532,
          "users": [
            {
              "id": "${server-password}"
            }
          ]
        }
      ]
    },
    "streamSettings": {
      "network": "tcp",
      "security": "tls",
      "tlsSettings": {
        "allowInsecure": true
      }
    },
    "mux": {
      "enabled": true,
      "concurrency": 8
    }
  },
  "policy": {
    "levels": {
      "0": {
        "uplinkOnly": 0
      }
    }
  }
}
```

- Server
```json
{
  "log": {
    "access": "/var/log/v2ray/access.log",
    "error": "/var/log/v2ray/error.log",
    "loglevel": "warning"
  },
  "transport": {
    "tcpSettings": {}
  },
  "inbound": {
    "port": 65532,
    "protocol": "vmess",
    "settings": {
      "clients": [
        {
          "id": "${server-password}",
          "level": 1,
          "alterId": 64,
          "email": "${user-email}"
        }
      ]
    },
    "streamSettings": {
      "network": "tcp",
      "security": "tls",
      "tlsSettings": {
        "certificates": [
          {
            "certificate": [
              "-----BEGIN CERTIFICATE-----",
              "${certificate-content...}",
              "-----END CERTIFICATE-----"
            ],
            "key": [
              "-----BEGIN RSA PRIVATE KEY-----",
              "${key-content...}",
              "-----END RSA PRIVATE KEY-----"
            ]
          }
        ]
      }
    },
    "detour": {
      "to": "dynamicPort"
    }
  },
  "inboundDetour": [
    {
      "tag": "dynamicPort",
      "protocol": "vmess",
      "port": "30000-40000",
      "settings": {
        "default": {
          "level": 1,
          "alterId": 32
        }
      },
      "allocate": {
        "strategy": "random",
        "concurrency": 2,
        "refresh": 3
      }
    }
  ],
  "outbound": {
    "protocol": "freedom",
    "settings": {}
  },
  "outboundDetour": [
    {
      "tag": "blocked",
      "protocol": "blackhole",
      "settings": {}
    }
  ],
  "routing": {
    "strategy": "rules",
    "settings": {
      "rules": [
        {
          "type": "field",
          "ip": [
            "0.0.0.0/8",
            "10.0.0.0/8",
            "100.64.0.0/10",
            "127.0.0.0/8",
            "169.254.0.0/16",
            "172.16.0.0/12",
            "192.0.0.0/24",
            "192.0.2.0/24",
            "192.168.0.0/16",
            "198.18.0.0/15",
            "198.51.100.0/24",
            "203.0.113.0/24",
            "::1/128",
            "fc00::/7",
            "fe80::/10"
          ],
          "outboundTag": "blocked"
        }
      ]
    }
  }
}
```