# Connect php with Oracle Database on CentOS 8
###### This tutorial will guide step by step to connect php with Oracle database. The steps are based on CentOS 8, but ithin it may work on any version as long as one can use yum and install rpm
#### Prereqisits:
- Installed CentOS 8
- Update the OS
- Install the php
In this case I have installed php 7.2 and php 5.6
The location of the php.ini is as follows:
> - php 7.2: /www/server/php/72/etc/php.ini
> - php 5.6: /www/server/php/56/etc/php.ini

Make directory and enter in it
`mkdir /opt/oracle
cd /opt/oracle`
wget https://yum.oracle.com/repo/OracleLinux/OL7/oracle/instantclient/x86_64/getPackage/oracle-instantclient19.9-basic-19.9.0.0.0-1.x86_64.rpm
wget https://yum.oracle.com/repo/OracleLinux/OL7/oracle/instantclient/x86_64/getPackage/oracle-instantclient19.9-devel-19.9.0.0.0-1.x86_64.rpm
yum install oracle-instantclient19.9-basic-19.9.0.0.0-1.x86_64.rpm
yum install oracle-instantclient19.9-devel-19.9.0.0.0-1.x86_64.rpm
pecl channel-update pecl.php.net
pecl install oci8
echo "extension =oci8.so" >> /www/server/php/72/etc/php.ini
sudo sh -c "echo /usr/lib/oracle/19.9/client64/lib > /etc/ld.so.conf.d/oracle.conf"
ldconfig
php -m | grep 'oci8'

for php 5

pecl install oci8-2.0.12
echo "extension =oci8.so" >> /www/server/php/56/etc/php.ini
sudo sh -c "echo /usr/lib/oracle/19.9/client64/lib > /etc/ld.so.conf.d/oracle.conf"
ldconfig
php -m | grep 'oci8'
