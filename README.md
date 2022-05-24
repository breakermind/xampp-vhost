# Xampp virtualhost SSL
Xampp virtualhost exmple

## Add local domain
C:\Windows\System32\drivers\etc\hosts
```sh
# app.xx
127.0.0.10 app.xx www.app.xx api.app.xx

# test.xx
# 127.0.0.11 test.xx www.test.xx api.test.xx
```

## Virtualhost laravel
```sh
<VirtualHost 127.0.0.10:80>        
    ServerName www.app.xx   
    
    # Redirect to https non-www
    Redirect permanent / https://app.xx/
    
    # Redirect to https non-www
    #RedirectMatch permanent ^/(.*)$ https://app.xx/$1

    # Redirect to https
    #RewriteEngine On
    #RewriteCond %{HTTPS} off
    #RewriteRule (.*) https://%{SERVER_NAME}$1 [R,L]
</VirtualHost>

<VirtualHost 127.0.0.10:80>    
    ServerName app.xx    
    
    DocumentRoot "D:/www/app.xx/public/"
    DirectoryIndex index.php

    ErrorLog "D:/www/app.xx/storage/logs/app.xx.error.log"
    CustomLog "D:/www/app.xx/storage/logs/app.xx.access.log" common

    # Redirect to https
    #RewriteEngine On
    #RewriteCond %{HTTPS} off
    #RewriteRule (.*) https://%{SERVER_NAME}$1 [R,L]

    <Directory "D:/www/app.xx/public">
        Options Indexes FollowSymLinks MultiViews
        AllowOverride all
        Order Deny,Allow
        Allow from all
        Require all granted
    </Directory>
</VirtualHost>

<VirtualHost 127.0.0.10:443>
    DocumentRoot D:/www/app.xx/public
    ServerName app.xx
    
    Protocols h2 http/1.1
    
    SSLEngine on
    SSLCertificateFile "conf/ssl.crt/server.crt"
    SSLCertificateKeyFile "conf/ssl.key/server.key"

    <Directory "D:/www/app.xx/public">
        Options Indexes FollowSymLinks MultiViews
        AllowOverride all
        Order Deny,Allow
        Allow from all
        Require all granted
    </Directory>
</VirtualHost>
```
