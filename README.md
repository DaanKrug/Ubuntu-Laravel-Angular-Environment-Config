# Ubuntu-Laravel-Angular-Environment-Config - Last update on: 21/03/2022
Simple Ubuntu Comands for Install a Laravel + Angular development environment: 
Apache2, PHP 7.4, Maria DB (mysql), NodeJs + NPM (Angular requirements).

This is a Step by Step for install and configure some programs. This is a compilation 
of various websites. The origin sites are above in right side
of each topic, there are the respectives descriptions.
Feel free to use this by yourself responsability. This is intended for use in development
machines.

======================================================================================

1º - Install Ubuntu Linux

======================================================================================

	# Make a bootable USB install
		- 1: Download an official ubuntu .iso file: 
			-On ubuntu: https://ubuntu.com/tutorials/create-a-usb-stick-on-ubuntu#download
			-On Windows: https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#download
		- 2: Transform the .iso file to bootable installation: 
			-On ubuntu: https://ubuntu.com/tutorials/create-a-usb-stick-on-ubuntu#1-overview
			-On Windows: https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview


======================================================================================

2º - Install Apache2 - https://thishosting.rocks/how-to-install-optimize-apache-ubuntu/

======================================================================================

sudo apt update

sudo apt upgrade

sudo apt install apache2 apache2-utils

sudo systemctl status apache2

sudo apachectl -v

sudo a2enmod rewrite allowmethods proxy proxy_http proxy_ajp deflate 
             headers proxy_balancer proxy_connect proxy_html

sudo systemctl restart apache2

sudo apt install curl

sudo apt install net-tools

sudo apt update

sudo apt upgrade

sudo gedit /etc/apache2/apache2.conf

   add the following, (after <Directory /var/www> section):

   <Directory /var/www/html>

      Options Indexes FollowSymLinks

      AllowOverride All

      AllowMethods OPTIONS HEAD GET POST PUT PATCH DELETE

      Require all granted

   </Directory>

sudo systemctl restart apache2

======================================================================================

3º - Install Maria DB - https://thishosting.rocks/install-mysql-mariadb-ubuntu/

======================================================================================

sudo apt install software-properties-common

sudo apt update

sudo apt install mariadb-server

sudo mysql 

	delete from mysql.user;

	insert into mysql.user(Host,User,Password,ssl_cipher,x509_issuer,x509_subject,authentication_string) values ('localhost','echo',PASSWORD('123456'),'','','','');
	
	GRANT ALL PRIVILEGES ON *.* TO 'echo'@'localhost';

	Flush Privileges;
	
	commit;
	
	exit;
	
sudo mysql -u echo -p123456


======================================================================================

4º - Install PHP 7.4 - https://thishosting.rocks/install-php-on-ubuntu/

======================================================================================

sudo apt update

sudo apt upgrade

sudo apt install php php7.4 php-pear php7.4-curl php7.4-xml php7.4-common php7.4-gd php7.4-intl php7.4-mbstring php7.4-zip php7.4-json php7.4-iconv php7.4-mysql php7.4-bcmath

sudo systemctl restart apache2



======================================================================================

5º - Install PhpMyAdmin as MariaDB client - https://www.phpmyadmin.net/

======================================================================================

download from https://www.phpmyadmin.net/

copy the .zip file to "/var/www/html"

sudo unzip <filezip>.zip 

sudo mv <filezip> mysql

Access http://localhost/mysql

cd /var/www/html/mysql

sudo cp config.sample.inc.php config.inc.php

sudo gedit config.inc.php

edit First server configuration section to seem as below:

/**

 * First server
 
 */
 
$i++;

/* Server parameters */

$cfg['Servers'][$i]['verbose'] = 'Local';

$cfg['Servers'][$i]['host'] = 'localhost';

$cfg['Servers'][$i]['port'] = '';

$cfg['Servers'][$i]['socket'] = '';

$cfg['Servers'][$i]['connect_type'] = 'tcp';

$cfg['Servers'][$i]['extension'] = 'mysqli';

$cfg['Servers'][$i]['auth_type'] = 'cookie';

$cfg['Servers'][$i]['AllowNoPassword'] = false;


=====================================================================================

6º - Install NodeJs/NPM - https://www.hostinger.com.br/tutoriais/instalar-node-js-ubuntu/

=====================================================================================

sudo apt update

sudo apt upgrade

sudo apt install nodejs

sudo apt install npm

sudo npm install -g @angular/cli

sudo npm cache clean -f

sudo npm install -g n

sudo n stable


=====================================================================================

7º - Install Laravel - https://laravel.com/

=====================================================================================

Install PHP composer: follow instructions on https://getcomposer.org/download/
 
composer create-project laravel/laravel example-app
 
cd example-app
 
php artisan serve




  