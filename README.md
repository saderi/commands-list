# UFW commands




| Description | command  |
| ------------ | -------------- |
| Allow specific Port | `ufw allow 6379`  |
| Allow Specific IP | `ufw allow from 203.0.113.4`|
| Allow Specific Port to specific IP | `ufw allow from 203.0.113.4 to any port 6379`|
| Allow Specific Port Ranges udp | `ufw allow 5000:5009/udp`  |
| Allow Specific Port Ranges tcp | `ufw allow 5000:5009/tcp`  |
| Allow Specific Port Ranges to to IP tcp | `ufw allow from 203.0.113.4 to any port 5000:5009 proto tcp`  |
| Deny all connections from Specific IP | `ufw deny from 203.0.113.4`  |
| ------------ | -------------- |
| Deny all outgoing traffic | `ufw default deny outgoing` |
| Allow all outgoing traffic | `ufw default allow outgoing` |
| Deny all incoming traffic | `ufw default deny incoming` |
| Allow all incoming traffic | `ufw default allow incoming` |


# Connection check

- IP count on port 80 & 443:

`netstat -anp | grep ':80\|:443' | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -n | wc -l`

- Connection count on port 80 & 443:

`netstat -an | grep ':80\|:443' | wc -l`


# Add Swap Space on Ubuntu 18.04

```
fallocate -l 4G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
cp /etc/fstab /etc/fstab.bak
echo '/swapfile none swap sw 0 0' | tee -a /etc/fstab
```

# PHP

- Find all php files and syntax check

`find . -iname "*.php" -print0 | xargs -0 -n1 php -l`



- Syntax check for laravel project

`find .  \( -path ./vendor -o -path ./node_modules -o -path ./storage -o -path ./.git \) -prune -o -name '*.php'  -print0 | xargs -0 -n1 php -l > /dev/null`


# System

Delete files older than 5 days

`find /tmp/* -type f -mtime +5 -exec rm -f {} +`

Delete files older than 5 minutes

`find /tmp/* -type f -mmin +5 -exec rm -f {} +`

chmod all folder to 755

`find /var/www/html -type d -print0 | xargs -0 chmod 755`

chmod all file to 644

`find /var/www/html -type f -print0 | xargs -0 chmod 644`


# Docker

#### Copy Docker images from one host to another without using a repository

Save the Docker image as a tar file:

`docker save -o TAR_FILE_PATH_AND_NAME IMAGE_NAME:TAG`

Copy your image to a new server and load the image into Docker:

`docker load -i TAR_FILE_PATH_AND_NAME`


# ETC

Convert cuttent folder subtitles to UTF8 Encoding

`for FILENAME in ./*.srt; do iconv -f cp1256 -t UTF-8 "${FILENAME}" -o "${FILENAME}"; done;`

