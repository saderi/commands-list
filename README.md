# UFW commands



| Description | command  |
| ------------ | ------------ |
| Allow specific Port | `ufw allow 6379`  |
| Allow Specific IP | `ufw allow from 203.0.113.4`|
| Allow Specific Port to specific IP | `ufw allow from 203.0.113.4 to any port 6379`|
| Allow Specific Port Ranges udp | `ufw allow 5000:5009/udp`  |
| Allow Specific Port Ranges tcp | `ufw allow 5000:5009/tcp`  |
| Allow Specific Port Ranges to to IP tcp | `ufw allow from 203.0.113.4 to any port 5000:5009 proto tcp`  |
| Deny all connections from Specific IP | `ufw deny from 203.0.113.4`  |


