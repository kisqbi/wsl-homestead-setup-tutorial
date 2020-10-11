**UPDATE & UPGRADE**

    sudo apt-get update && sudo apt dist-upgrade
**install nginx**

    sudo apt install nginx

 **install mysql**

    sudo apt install mysql
    sudo usermod -d /var/lib/mysql/ mysql
    sudo service mysql start
    sudo mysql_secure_installation

Say **no** to the first prompt: **VALIDATE PASSWORD PLUGIN**, input and confirm your new mysql password and say **yes** to the rest of inputs.



    sudo apt-get install php7.4-cli php7.4-fpm php7.4-curl php7.4-gd php7.4-mysql php7.4-mbstring php7.4-json php7.4-xml php7.4-bcmath zip unzip

**nano ~/.bashrc**    

    # Start Nginx, PHP 7.2 and MySQL on boot
    sudo /etc/init.d/nginx start  
    sudo /etc/init.d/php7.2-fpm start  
    sudo /etc/init.d/mysql start

**sudo visudo**

    # Programs that will start automatically  
    %sudo ALL=NOPASSWD: /etc/init.d/nginx  
    %sudo ALL=NOPASSWD: /etc/init.d/php7.2-fpm  
    %sudo ALL=NOPASSWD: /etc/init.d/mysql

**mysql -uroot**

    CREATE DATABASE `laravel` CHARACTER SET utf8 COLLATE utf8_general_ci;
    CREATE USER 'laravel_user'@'%' IDENTIFIED BY 's3cr3t';
    USE LARAVEL;
    GRANT ALL ON `laravel.*` TO 'laravel_user'@'%';
    FLUSH PRIVILEGES;
**create project**

    composer create-project --prefer-dist laravel/laravel example
**Setting up Permissions**

    sudo chown -R <your_username>:www-data /home/<your_username>/examplesudo chmod -R 777 /home/<your_username>/example

**host file** 

    127.0.0.1 example.local

**Setting up the Nginx block**

    sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/example.localsudo nano /etc/nginx/sites-available/example.local
    sudo ln -s /etc/nginx/sites-available/example.local /etc/nginx/sites-enabled/example.local

**laravel site config**
```php
server {
    listen 80;
    server_name example.com;
    root /srv/example.com/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

