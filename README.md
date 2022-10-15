# List:
* [UFW commands](#ufw-commands)
* [Port and Connection check](#port-and-connection-check)
* [Add Swap Space on Ubuntu 18.04](#add-swap-space-on-ubuntu-1804)
* [PHP](#php)
* [MySQL Commands](#mysql-commands)
* [Files](#files-tools)
* [Docker](#docker)
* [GPG Encrypting and decrypting file](#gpg-encrypting-and-decrypting-file)
* [HTTPS/SSL](#https-ssl)
* [ETC](#etc)

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

# Port and Connection check

### IP count on port 80 & 443:

`netstat -anp | grep ':80\|:443' | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -n | wc -l`

### Connection count on port 80 & 443:

`netstat -an | grep ':80\|:443' | wc -l`

### Find Out What Is Using TCP Ports

`netstat -tulpn`

### Checking port with netcat

`nc -vz -w 5 142.250.203.110 443`

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

### Find all php files and syntax check

`find . -iname "*.php" -print0 | xargs -0 -n1 php -l`



### Syntax check for laravel project

`find .  \( -path ./vendor -o -path ./node_modules -o -path ./storage -o -path ./.git \) -prune -o -name '*.php'  -print0 | xargs -0 -n1 php -l > /dev/null`

<a name="mysql_commands"></a>
# MySQL Commands

### Size of specified database in MB
```
SELECT table_schema ,
    ROUND(SUM(data_length + index_length) / 1024 / 1024, 1) "DB Size in MB" 
    FROM information_schema.tables  WHERE table_schema='DB_NAME'
    GROUP BY table_schema ;
```

<a id="files-tools"></a>
# Files

### Delete files older than 5 days

`find /tmp/* -type f -mtime +5 -exec rm -f {} +`

### Delete files older than 5 minutes

`find /tmp/* -type f -mmin +5 -exec rm -f {} +`

### chmod all folder to 755

`find /var/www/html -type d -print0 | xargs -0 chmod 755`

### chmod all file to 644

`find /var/www/html -type f -print0 | xargs -0 chmod 644`

### Single line loop

`for i in {a..z}; do YOUR_COMMAND; done`

or

`for((i=1;i<=100;i+=5)); do echo "Hi ${i}"; done`

### Change multiple files extensions in recursive folders

`find . -name '*.xtA' -exec bash -c 'mv "$0" "${0%.xtA}.xtB"' "{}" \;`

### Get files/folders size, include hidden files/folders with `du` command [ [source](https://askubuntu.com/a/363681) ]
`du -sch .[!.]* * |sort -h`

<a name="docker"></a>
# Docker

#### Copy Docker images from one host to another without using a repository

### Save the Docker image as a tar file:

`docker save -o TAR_FILE_PATH_AND_NAME IMAGE_NAME:TAG`

### Copy your image to a new server and load the image into Docker:

`docker load -i TAR_FILE_PATH_AND_NAME`

<a name="gpg_commands"></a>
# GPG Encrypting and decrypting file

### Generate a new keypair
`gpg --full-generate-key`

### Export the keypair to a file
`gpg --export -a "EMAIL OR KEY_NAME" > public.key`

### Import public key to your keystore
`gpg --import someone_public.key`

### Encrypt EXAMPLE.gz File 
`gpg --output ENCRYPTED_EXAMPLE.gpg --recipient "EMAIL OR KEY_NAME" --armor --always-trust --encrypt EXAMPLE.gz`

### Decrypt EXAMPLE.gz File 
`gpg --output EXAMPLE.gz --recipient "EMAIL OR KEY_NAME" --decrypt ENCRYPTED_EXAMPLE.gpg`

<a name="https-ssl"></a>
# HTTPS/SSL 

### Check SSL KEY and CRT files relation 
If the output of both commands is equal, privet key and ssl certificate are related
```
openssl x509 -noout -modulus -in domain.crt.pem | openssl md5
openssl rsa -noout -modulus -in domain.privet_key.pem | openssl md5
```

### Extracting the certificate and keys from a .pfx file
The .pfx file, which is in a PKCS#12 format, contains the SSL certificate (public keys) and the corresponding private keys

Extract the private key (this key is encrypted)
```
openssl pkcs12 -in [YOUR_FILE.pfx] -nocerts -out encrypted_private_key.pem
```
Extract the certificate
```
openssl pkcs12 -in [YOUR_FILE.pfx] -clcerts -nokeys -out certificate.pem
```
Decrypt the encrypted private key
```
openssl rsa -in encrypted_private_key.pem -out decrypted_private_key.pem
```

<a name="etc"></a>
# ETC

### Convert cuttent folder subtitles to UTF8 Encoding

`for FILENAME in ./*.srt; do iconv -f cp1256 -t UTF-8 "${FILENAME}" -o "${FILENAME}"; done;`

### Merge / convert multiple PDF files into one PDF [ [source](https://stackoverflow.com/a/2507825/1987553) ]

`pdftk file1.pdf file2.pdf cat output output.pdf`

### Convert larg video to smaller video

`ffmpeg -i inputfile.mp4 -acodec aac  -s 1366x768   inputfile_smaller.mp4`

### Breaking large file into small pieces and reassemble them
#### split
```
$ split --verbose -b500M large_2.4GB_file.tar small_600MB_files.tar.
creating file 'small_600MB_files.tar.aa'
creating file 'small_600MB_files.tar.ab'
creating file 'small_600MB_files.tar.ac'
creating file 'small_600MB_files.tar.ad'
creating file 'small_600MB_files.tar.ae'
```
#### reassemble
`cat small_600MB_files.tar.a? > large_2.4GB_file.tar`



