<!-- TITLE: Webserver Configs -->
<!-- SUBTITLE: A quick summary of Webserver Configs -->

# Webserver Configs


## Apache 

### Nextcloud


```apache_conf
<VirtualHost *:444>
        ServerName localhost 
        #ServerAlias findsomebuddy.de

        # Logging
        LogLevel warn
        ErrorLog /var/log/httpd/petitcoderoot-error_log
        CustomLog /var/log/httpd/petitcoderoot-access_log combined

        # SSL Configuration - uses strong cipher list - these might need to be downgraded if you need to support older browsers/devices
        SSLEngine on
        SSLProxyEngine On
        SSLCipherSuite EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH
        SSLProtocol All -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
        SSLHonorCipherOrder On
        SSLCertificateFile /etc/letsencrypt/archive/petitcode.com/cert1.pem
        SSLCertificateKeyFile /etc/letsencrypt/archive/petitcode.com/privkey1.pem
        SSLCertificateChainFile /etc/letsencrypt/archive/petitcode.com/chain1.pem
        DocumentRoot /var/www/html/nextcloud


        # HSTS (optional)
        Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains;"
        # Remove this if you need to use frames or iframes
        #Header always set X-Frame-Options DENY
        # Prevent MIME based attacks
        Header set X-Content-Type-Options "nosniff"
        # Reverse proxy configuration
        Header set X-Frame-Options: "sameorigin"

#       Alias /nextcloud "/var/www/html/nextcloud/"
        <Directory /var/www/html/nextcloud/>
                Options +FollowSymlinks
                AllowOverride All
                <IfModule mod_dav.c>
                        Dav off
                </IfModule>
                SetEnv HOME /var/www/html/nextcloud
                SetEnv HTTP_HOME /var/www/html/nextcloud
        </Directory>
</VirtualHost>
```



## Nginx

### Nextcloud


```apache_conf
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name  nextcloud.petitcode.com;

    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:50m;
    ssl_session_tickets off;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH EDH+aRSA !RC4 !aNULL !eNULL !LOW !3DES !MD5 !EXP !PSK !SRP !DSS";
    ssl_prefer_server_ciphers on;

    
ssl_certificate_key /etc/letsencrypt/live/petitcode.com/privkey.pem;


    ssl_certificate /etc/letsencrypt/live/petitcode.com/fullchain.pem;


    ssl_trusted_certificate   /etc/letsencrypt/live/petitcode.com/chain.pem;
 


    location / {
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_pass https://localhost:444;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_next_upstream error timeout http_502 http_503 http_504;
    }

}


```

### Wiki JS


```apache_conf
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name  wiki.petitcode.com;

    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:50m;
    ssl_session_tickets off;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH EDH+aRSA !RC4 !aNULL !eNULL !LOW !3DES !MD5 !EXP !PSK !SRP !DSS";
    ssl_prefer_server_ciphers on;
    ssl_certificate_key /etc/letsencrypt/live/petitcode.com/privkey.pem;
    ssl_certificate /etc/letsencrypt/live/petitcode.com/fullchain.pem;
    ssl_trusted_certificate   /etc/letsencrypt/live/petitcode.com/chain.pem;
 
    location / {
       proxy_ssl_server_name on; 

        proxy_set_header Host $http_host;
        proxy_set_header X_FORWARDED_PROTO https;
        proxy_ssl_trusted_certificate /etc/letsencrypt/live/petitcode.com/fullchain.pem;
        proxy_ssl_verify              on;
        proxy_ssl_verify_depth 2;
        proxy_pass http://127.0.0.1:3001;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_next_upstream error timeout http_502 http_503 http_504;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Real-IP $remote_addr;

        }
}

```



# Wiki js Fix
There was really a Problem to config nginx and apache for the wikijs. Nginx always calling bad gateway if we set the proxy pass to https and another port then 443, but we have do, because apache is listen to 443, too.
So i wrote some code hard in the wikijs instance : 


```batchfile
[root@petitcoderoot server]# grep -rn vendor.js
views/auth/login.pug:21:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')
views/error-notexist.pug:21:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')
views/configure/index.pug:16:    script(type='text/javascript', src='/js/vendor.js')
views/layout.pug:26:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')
views/error.pug:21:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')
views/error-forbidden.pug:21:    script(type='text/javascript', src='https://wiki.petitcode.com/js/vendor.js')


[root@petitcoderoot server]# grep -rn app.js
views/auth/login.pug:22:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')
views/error-notexist.pug:22:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')
views/layout.pug:27:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')
views/error.pug:22:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')
views/error-forbidden.pug:22:    script(type='text/javascript', src='https://wiki.petitcode.com/js/app.js')

```


I wrote the Url : https://wiki.petitcode.com/js/vendor.js hard in the Files which are be greped. So i garanty of right serving of the vendor.js and the app.js!
Else there is no css loading.

