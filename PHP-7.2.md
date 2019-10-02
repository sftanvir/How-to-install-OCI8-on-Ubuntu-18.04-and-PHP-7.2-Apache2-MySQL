## How to install OCI8 on Ubuntu 18.04 and PHP-7.2, Apache2 and MySQL
The procedure covers the installation a basic report server which can pull data from Oracle using php 7.2

Update the OS
```
apt-get update
apt-get upgrade -y
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
apt-get -y install apache2 apache2-doc apache2-utils libapache2-mod-php php7.2 php7.2-common php7.2-gd php7.2-mysql php7.2-imap phpmyadmin php7.2-cli php7.2-cgi libapache2-mod-fcgid apache2-suexec-pristine php-pear mcrypt  imagemagick libruby libapache2-mod-python php7.2-curl php7.2-intl php7.2-pspell php7.2-recode php7.2-sqlite3 php7.2-tidy php7.2-xmlrpc php7.2-xsl memcached php-memcache php-imagick php-gettext php7.2-zip php7.2-mbstring php-soap php7.2-soap
apt-get -y install php-dev php-pear build-essential libaio1
```
Install php opcache and fmp
```
apt-get -y install php7.2-opcache php-apcu
apt-get -y install php7.2-fpm
service apache2 restart
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
pecl install oci8
```
when it asks for location, paste it
```
instantclient,/opt/oracle/instantclient_19_3
```
Enable php extensions
```
echo "extension =oci8.so" >> /etc/php/7.2/fpm/php.ini
echo "extension =oci8.so" >> /etc/php/7.2/cli/php.ini
echo "extension =oci8.so" >> /etc/php/7.2/apache2/php.ini
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
