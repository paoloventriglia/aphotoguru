# Simple LAMP Web Application

If you are using Ubuntu 16.04

~~~~
sudo apt-get -y update
sudo apt-get -y install git mysql-server
sudo apt-get -y install apache2 php libapache2-mod-php php-mcrypt php-mysql php-curl php-xml php-memcached
sudo systemctl restart apache2
~~~~

Then we clone the source code from git repository.

~~~~
cd /var/www/html
sudo git clone https://github.com/paoloventriglia/aphotoguru
~~~~

Then we create a MySQL database and a MySQL user for our demo. Here we use “web_demo” as the database name, and “username” as the MySQL user.

~~~~
sudo mysql -u root -e "CREATE DATABASE aphotoguru;"
sudo mysql -u root -e "CREATE USER 'guru'@'localhost' IDENTIFIED BY 'Ph0t0';"
sudo mysql -u root -e "GRANT ALL PRIVILEGES ON aphotoguru.* TO 'guru'@'localhost';"
sudo mysql -u root -e "FLUSH PRIVILEGES;"
sudo mysql -u root -e "SET PASSWORD FOR 'root'@'localhost' = PASSWORD('Pa55w0rd');"
sudo systemctl restart mariadb
sudo systemctl restart mysql
~~~~

Setup the DB

Change the ownership of folder “uploads” to “www-data” so that Apache can upload files to this folder.

~~~~
cd /var/www/html/aphotoguru
sudo mysql -u guru -pPh0t0 aphotoguru < db_setup.sql
sudo chown -R www-data:www-data uploads
~~~~

In your browser, browse to http://ip-address/aphotoguru/index.php. You should see that our application is now working. 

