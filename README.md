# dockerapachephp
# Docker Apache2

## Setup

```
docker compose up -d
hoặc docker-compose up -d
d
```

## Build images and push images to docker hub

```
docker build -t phamphu232/php:7.3 -f ./php7.3/Dockerfile .
docker push phamphu232/php:7.3
```

## Example VirtualHost

```
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
