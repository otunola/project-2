# project-2  LEMP STACK IMPLEMENTATION
1. After the ubunter server creation on AWS,start off by updating your server’s package index with the following command : sudo apt update
2. then intall NgiNx  web server with the command : sudo apt install nginx
3. confirm the status of the installation with the command : sudo systemctl status nginx 
as shown below
<img width="562" alt="Screen Shot 2022-09-03 at 4 48 53 PM" src="https://user-images.githubusercontent.com/112595648/188312297-9238003b-4f2d-47d0-8e56-ceced8028ba7.png">

4. open the TCP port 80 of the EC2 instance on AWS as shown below so as to allow traffic flow on port 80, 

<img width="1109" alt="Screen Shot 2022-09-03 at 5 06 32 PM" src="https://user-images.githubusercontent.com/112595648/188312380-b413881f-d939-4239-9400-f856d6cfbea4.png">

5. checked if can access the port 80 from the ubuntu with the command : curl http://127.0.0.1:80
<img width="565" alt="Screen Shot 2022-09-03 at 5 19 06 PM" src="https://user-images.githubusercontent.com/112595648/188313080-f70d8f6a-7f44-48be-863c-f99365b86d05.png">

6. also try to access the server ip address on the URL

<img width="1095" alt="Screen Shot 2022-09-03 at 5 20 45 PM" src="https://user-images.githubusercontent.com/112595648/188313308-1af44cc6-1a7d-4b31-9d57-cce941377466.png">
7. Since NginX works well now we install a server to handle the database for the web server. we use mysql and will install with the command
 : sudo apt install mysql-server
8. after installation is finished, log in to the MySQL console by typing: sudo mysql

9.  Run a security script that comes pre-installed with MySQL. This  will remove some insecure default settings and put a password unto the database:
: ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
10. the password of the database is now set to PassWord.1

11.the database can now be accessed with the command : sudo mysql -p
 and the password will be required to access it because of the -p
 12. Your MySQL server is now installed and secured. Next, we will install PHP, the final component in the LEMP stack.

13. Since NginX is properly installed, Now you can install PHP to process code and generate dynamic content for the web server.
   the packages needed will be installed with this command : sudo apt install php-fpm php-mysql
14. the version of the php installation can be checked with the command : php -v
You now have your PHP components installed. Next, you will configure Nginx to use them.

 To encapsulate configuration details and host more than one domain on a single server. in this project we create another directory to add to the default one instead of modifying the default.
 
 15. the new directory is named projectLEMP and created witht the command : sudo mkdir /var/www/projectLEMP
 16. Assign ownership of the directory with the current user : sudo chown -R $USER:$USER /var/www/projectLEMP

We then use nano to create a new site for Nginx’s sites-available with the command : sudo nano /etc/nginx/sites-available/projectLEMP

17. We paste and save the following component
18. #/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}

19. Activate your configuration by linking to the config file from Nginx’s sites-enabled directory with the command 
    :sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/


