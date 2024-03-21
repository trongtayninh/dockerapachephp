# dockerapachephp
# Docker Apache2

## Setup
```
docker ps 
docker kill $(docker ps -q)  xoá hết các container đang chạy 
danh sách các image đang có 
docker images
xoá 1 images
docker rmi -f 4ca9e333ffa3

Error:
Error response from daemon: Conflict. The container name "/con_ap_apache2" is already in use by container "ead774a142a9594cedd619721a2f80a8ac8821ac3ab6a637c87e72336d28ce6a". You have to remove (or rename) that container to be able to reuse that name
docker stop con_ap_apache2
docker rm con_ap_apache2

docker logs con_ap_apache2	
comment cái này lại F:\learn\apache2php82\docker-compose.yml	
- ./apache2:/etc/apache2	
	
	
 docker compose down	
docker compose up -d	

```
```
docker compose up -d
hoặc docker-compose up -d


```

## Build images and push images to docker hub

```
docker build -t phamphu232/php:7.3 -f ./php7.3/Dockerfile .
docker push phamphu232/php:7.3
```

## Example VirtualHost

```
nano /etc/hosts
127.0.0.1 mytest.local
127.0.0.1 mytest82.local
curl mytest.local:8080/index.php
cd /var/www/dockerapachephp-main
 docker compose restart

<VirtualHost *:80>
  ServerAdmin         phamphu232@gmail.com
  ServerName          hello-world.local
  DocumentRoot        /var/www/hello-world/public

  ErrorLog  /var/log/apache2/hello-world-error_log
  CustomLog /var/log/apache2/hello-world-access_log common

  # SSLEngine on
  # SSLCertificateFile	/etc/certs/self-signed.crt
  # SSLCertificateKeyFile /etc/certs/self-signed.key

  <Directory "/var/www/hello-world/public">
    Options FollowSymLinks
    AllowOverride All
    # Order allow,deny
    Require all granted
    Allow from all
  </Directory>

  <FilesMatch \.php$>
    # For Apache version 2.4.10 and above, use SetHandler to run PHP as a fastCGI process server
    SetHandler "proxy:fcgi://php73:9000"
    # SetHandler "proxy:unix:/run/php/php7.3-fpm.sock|fcgi://php73:9000"
  </FilesMatch>
</VirtualHost>
```
