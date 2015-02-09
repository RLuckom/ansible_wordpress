# Ansible Playbook for deploying WordPress

This deploys a LAMP stack including PHP 5.5, Apache, and MySQL >= 14.

Additionally, it takes an existing WordPress installation, comprising:

- MySQL username, databasename, and password (in a separate file, .gitignored)
- Intended  MySQL username, databasename, and password (in the above file)
- WordPress installation root directory (specified at the commandline)
- Current hostname
- Intended hostname
- Host address (specified in hosts or ~/.ssh/config)

and migrates it onto the new host.

php5-gd
php5-mysql
libapache2-mod-php5
mysql-server-5.6
apache2

### Todo:

 - [ ] MySQL
  - [ ] dump current db to tmp file - mysqldump -u { current-user } {
    current-database } > { dumpfile }.sql
  - [ ] Install - apt-get install mysql-server-5.6
  - [ ] Set up database
   - [ ] add { site-name } with { password } - CREATE USER '{ site-name }'@'localhost'
     IDENTIFIED BY '{ password }';
   - [ ] create database - CREATE DATABASE { site-name };
   - [ ] grant user privs - GRANT ALL PRIVILEGES ON { site-name }.\* to '{
     site-name }@'localhost'
   - [ ] scp dump from original
   - [ ] load dump from original - cat { dumpfile }.sql | mysql -u { site-name }
     { site-name }
   - [ ] update hostnames in database - see update script
 - [ ] Apache
  - [ ] Install - apt-get install apache2
  - [ ] Configure
   - [ ] a2enmod rewrite
   - [ ] AllowOverride /var/wwww in apache2.conf
   - [ ] Add VirtualHost in sites-available
    - [ ] Route in VirtualHost tag, e.g. '\*:8080'
    - [ ] DocumentRoot within VirtualHost: /var/www/{site-name}
    - [ ] ErrorLog within VirtualHost: ${APACHE\_LOG\_DIR}/{site-name}-error.log
    - [ ] Access log within VirtualHost: CustomLog ${APACHE\_LOG\_DIR}/tim-neill-access.log combined
 - [ ] PHP
  - [ ] Install - apt-get install php5 php5-gd php5-mysql libapache-mod-php5
 - [ ] WordPress
  - [ ] mkdir /var/www/{ site-name }
  - [ ] get Wordpress
   - [ ] Fresh install or copy wholesale?
   - [ ] Set up config vars
    - [ ] DB\_NAME: { site-name }
    - [ ] DB\_USER: { site-name }
    - [ ] DB\_PASSWORD: { password }
    - [ ] AUTH\_KEY: { random chars }
    - [ ] SECURE\_AUTH\_KEY: { random chars }
    - [ ] LOGGED\_IN\_KEY: { random chars }
    - [ ] NONCE\_KEY: { random chars }
    - [ ] AUTH\_SALT: { random chars }
    - [ ] SECURE\_AUTH\_SALT: { random chars }
    - [ ] LOGGED\_IN\_SALT: { random chars }
    - [ ] NONCE\_SALT: { random chars }
  - [ ] Copy wp-content if not already done 
