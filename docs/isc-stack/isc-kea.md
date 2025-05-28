# Install ISC-KEA DHCP4 on Ubuntu 22.04

### Update Repository

```bash
sudo apt update && sudo apt upgrade
```

```bash
sudo apt install curl apt-transport-https
```

### Adding ISC KEA Repository

```bash
curl -1sLf https://dl.cloudsmith.io/public/isc/kea-2-6/setup.deb.sh | sudo -E bash
```

```bash
sudo apt update
```

### Install KEA DHCP

```bash
sudo apt install isc-kea
```

### Check the version and service status

```bash
kea-dhcp4 -version
```

**To check the service and confirm it is running without any error**

For DHCP4

```bash
systemctl status isc-kea-dhcp4-server
```

For DHCP6

```bash
systemctl status isc-kea-dhcp6-server
```

**Enable the service to start on boot**

For DHCP4

```bash
sudo systemctl enable isc-kea-dhcp4-server
```

For DHCP6

```bash
sudo systemctl enable isc-kea-dhcp6-server
```

## Example configuration for DHCP4

Before setup, backup default config file first

```bash
sudo mv /etc/kea/kea-dhcp4.conf /etc/kea/kea-dhcp4.conf.bak
```

Now, create the new configuration file in your preferred text editor

```bash
sudo nano /etc/kea/kea-dhcp4.conf
```

```
{
  "Dhcp4": {
    "interfaces-config": {
      "interfaces": [
        "eth0"
      ]
    },
    "control-socket": {
      "socket-type": "unix",
      "socket-name": "/tmp/kea4-ctrl-socket"
    },
    "lease-database": {
      "type": "memfile",
      "persist": true,
      "name": "/tmp/dhcp4.leases"
    },
    "valid-lifetime": 28800,
    "option-data": [
      {
        "name": "domain-name-servers",
        "data": "192.0.2.1, 192.0.2.2"
      }
    ],
    "client-classes": [
      {
        "name": "voip",
        "test": "substring(option[60].hex,0,6) == 'SomePhone'",
        "next-server": "192.0.2.254",
        "server-hostname": "hal9000",
        "boot-file-name": "SomePhone-settings.cfg"
      }
    ],
    "hooks-libraries": [
      {
        "library": "/path/libdhcp_lease_cmds.so"
      },
      {
        "library": "/path/libdhcp_ha.so",
        "parameters": {
            "high-availability": [
              {
                "this-server-name": "server1",
                "mode": "hot-standby",
                "peers": [
                  {
                    "name": "server1",
                    "url": "http://192.168.56.33:8000/",
                    "role": "primary",
                    "auto-failover": true
                },
                {
                    "name": "server2",
                    "url": "http://192.168.56.66:8000/",
                    "role": "standby",
                    "auto-failover": true
                }
              ]
            }
          ]
        }
      }
    ],
    "subnet4": [
      {
        "subnet": "192.0.2.0/24",
        "pools": [
          {
            "pool": "192.0.2.1 - 192.0.2.200"
          }
        ],
        "option-data": [
          {
            "name": "routers",
            "data": "192.0.2.1"
          }
        ],
        "reservations": [
          {
            "hw-address": "1a:1b:1c:1d:1e:1f",
            "ip-address": "192.0.2.201",
            "option-data": [
              {
                "name": "domain-name-servers",
                "data": "10.1.1.202, 10.1.1.203"
              }
            ]
          }
        ]
      }
    ],
    "loggers": [
      {
        "name": "kea-dhcp4",
        "output_options": [
          {
            "output": "/tmp/kea-dhcp4.log",
            "maxsize": 1048576,
            "maxver": 8
          }
        ],
        "severity": "INFO"
      },
      {
        "name": "kea-dhcp4.packets",
        "output_options": [
          {
            "output": "/tmp/kea-dhcp4-packets.log",
            "maxver": 10
          }
        ],
        "severity": "DEBUG",
        "debuglevel": 99
      }
    ]
  }
}
```
