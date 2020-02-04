Install adminer nginx ubuntu

First, you need to create a directory inside /usr/share folder using the following command

**sudo mkdir /usr/share/adminer**
To get an updated version of adminer use following command:

sudo wget "http://www.adminer.org/latest.php" -O /usr/share/adminer/latest.php
Now go to your Nginx default file of nginx and paste the following code

location /adminer {
   root /usr/share/;
            index index.php index.html index.htm;
            location ~ ^/adminer/(.+\.php)$ {
       try_files $uri $uri/ /index.php?$query_string;
                fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
                include fastcgi_params;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            }
}
Simple restart your nginx server using the following commands sudo service nginx restart

