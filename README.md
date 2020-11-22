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



# Connection check

- Uniq IP count on port 80 & 443:

`netstat -anp \| grep ':80\|:443' \| awk '{print $5}' \| cut -d: -f1 \| sort \| uniq -c \| sort -n \| wc -l`

- Connection count on port 80 & 443:

`netstat -an | grep ':80\|:443' | wc -l`
