# ubuntu-20-04-php-53-fpm
If you want to use legacy version of php 5.3 with php-fpm and want to configure nginx on ubuntu 20.04 server than it is for you.

##Step 1
install nginx
`sudo apt-get install -y nginx`
add php5.3 repo
`sudo add-apt-repository ppa:sergey-dryabzhinsky/php53`
`sudo apt-get update`
`sudo apt-get install -y php5`
`sudo apt-get install -y php53-fpm`

## Step 2
