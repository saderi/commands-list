# UFW commands

allow specific port too all IP : 



| Description | command  |
| ------------ | ------------ |
| Allow specific Port | `ufw allow zz`  |
| Specific IP Addresses | `ufw allow from xxx.xxx.xxx.xxx`|
| Specific Port to specific IP Address | `ufw allow from xxx.xxx.xxx.xxx to any port zz`|
| Specific Port Ranges udp | `ufw allow 6000:6007/udp`  |
| Specific Port Ranges tcp | `ufw allow 6000:6007/tcp`  |
| Specific Port Ranges to to IP Address tcp | `ufw allow from xxx.xxx.xxx.xxx to any port 6000:6007 proto tcp`  |


