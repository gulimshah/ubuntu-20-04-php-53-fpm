# ubuntu 20.04 and php53-fpm
If you want to use legacy version of php 5.3 with php-fpm and want to configure nginx on ubuntu 20.04 server than it is for you.

##Step 1
install nginx 
```
sudo apt-get install -y nginx
```
## Step 2
Add php 5.3 repo and subsequently  install php with php-fpm
```
sudo add-apt-repository ppa:sergey-dryabzhinsky/php53
sudo apt-get update 
sudo apt-get install -y php5 
sudo apt-get install -y php53-fpm
```
## Step 3
Rename the default php53-fpm pool-www-data config file
```
sudo mv /etc/php53/fpm/pool-www-data.conf.example pool-www-data.conf
```
Open pool-www-data.conf file and change the following:
`listen = /var/run/php5-fpm.sock` directive with `Listen 127.0.0.1:9000`
`prefix = /var/www/html`
`chdir =/var/www/html`

## Step 4
Similarly adjust the `/etc/nginx/sites-available/default` php directive to listen 127.0.0.1:9000 instead of sock file

```
location ~ \.php$ {
               include snippets/fastcgi-php.conf;
        #
        #       # With php7.0-cgi alone:
               fastcgi_pass 127.0.0.1:9000;
        #       # With php7.0-fpm:
        #       fastcgi_pass unix:/run/php/php53-fpm.sock;
        }
```
## Step 5
change the permission of following directories to editable by php53-fpm and Nginx
```
sudo chmod 777 -R /var/www/html
sudo chmod 777 -R /var/log/php53-fpm
```
## Final Step
Restart the services
```
sudo systemctl restart nginx.service
sudo systemctl restart php53-fpm.service
```
