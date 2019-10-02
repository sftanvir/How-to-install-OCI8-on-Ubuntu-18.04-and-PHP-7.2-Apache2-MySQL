## How to install OCI8 on Ubuntu 18.04 and PHP-5.6, Apache2 and MySQL
The procedure covers the installation a basic report server which can pull data from Oracle using php 7.2

Add repository. This point is very inportant as php5.6 is not supported anymore
```
apt-get install python-software-properties
add-apt-repository ppa:ondrej/php
```
Update the OS
```
apt-get update
apt-get upgrade -y
```
Install ntp and change time zone to Asia/Dhaka
```
apt-get install ntp ntpdate
timedatectl list-timezones
timedatectl set-timezone Asia/Dhaka
```
Install network tools and MariaDB
```
apt install net-tools
apt-get -y install mariadb-client mariadb-server
mysql_secure_installation
```
Restart the MariaDB
```
service mysql restart
```
Install php along with some extensions
```
apt-get -y install apache2 apache2-doc apache2-utils libapache2-mod-php5.6 php5.6 php5.6-common php5.6-gd php5.6-mysql php5.6-imap phpmyadmin php5.6-cli php5.6-cgi libapache2-mod-fcgid apache2-suexec-pristine php-pear mcrypt imagemagick libruby libapache2-mod-python php5.6-curl php5.6-intl php5.6-pspell php5.6-recode php5.6-sqlite3 php5.6-tidy php5.6-xmlrpc php5.6-xsl memcached php-memcache php-imagick php-gettext php5.6-zip php5.6-mbstring php-soap php5.6-soap
apt-get -y install php5.6-dev php5.6-pear build-essential libaio1
```
Procedure for OCI8 installation
```
mkdir /opt/oracle
cd /opt/oracle
```
Download oracle instant client basic
```
wget https://download.oracle.com/otn_software/linux/instantclient/193000/instantclient-basic-linux.x64-19.3.0.0.0dbru.zip
```
Download oracle instant client sdk
```
wget https://download.oracle.com/otn_software/linux/instantclient/193000/instantclient-sdk-linux.x64-19.3.0.0.0dbru.zip
```
Unzip both of them
```
unzip instantclient-basic-linux.x64-19.3.0.0.0dbru.zip 
unzip instantclient-sdk-linux.x64-19.3.0.0.0dbru.zip 
```
Creat Links
```
ln -s /opt/oracle/instantclient_19_3/libclntsh.so.12.1 /opt/oracle/instantclient_19_3/libclntsh.so
ln -s /opt/oracle/instantclient_19_3/libocci.so.12.1 /opt/oracle/instantclient_19_3/libocci.so
```

```
echo /opt/oracle/instantclient_19_3 > /etc/ld.so.conf.d/oracle-instantclient
ldconfig
```
```
pecl channel-update pecl.php.net
pecl install oci8-2.0.12
```
when it asks for location, paste it
```
instantclient,/opt/oracle/instantclient_19_3
```
Enable php extensions
```
echo "extension =oci8.so" >> /etc/php/5.6/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/5.6/cli/php.ini
echo "extension =oci8.so" >> /etc/php/5.6/apache2/php.ini
echo "export LD_LIBRARY_PATH=/opt/oracle/instantclient_19_3" >> /etc/apache2/envvars
echo "export ORACLE_HOME=/opt/oracle/instantclient_19_3" >> /etc/apache2/envvars
echo "LD_LIBRARY_PATH=/opt/oracle/instantclient_19_3:$LD_LIBRARY_PATH" >> /etc/environment
export LD_LIBRARY_PATH=/opt/oracle/instantclient_19_3
```
```
sh -c "echo /opt/oracle/instantclient_19_3 > /etc/ld.so.conf.d/oracle-instantclient.conf"
ldconfig
```
Run this command, if it shows 
```
php -m | grep 'oci8'
```
oci8
Then you are good to go...
