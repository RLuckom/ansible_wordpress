# Ansible Playbook for deploying WordPress on remote Ubuntu

This deploys a LAMP stack including PHP 5.5, Apache, and MySQL >= 14.

Additionally, it takes an existing WordPress installation, comprising:

- Location of mysqldump of the current db
- Intended  MySQL username, databasename, and password (in the above file)
- WordPress installation root directory (specified at the commandline)
- Current hostname
- Intended hostname
- Host address (specified in hosts or ~/.ssh/config)

and migrates it onto the new host.

Based heavily on lamp\_simple from
[ansible-examples](https://github.com/ansible/ansible-examples/)

### Todo:

 - [x] MySQL
  - [x] Install - apt-get install mysql-server-5.6
  - [x] Set up database
   - [x] add { site-name } with { password } - CREATE USER '{ site-name }'@'localhost'
     IDENTIFIED BY '{ password }';
   - [x] create database - CREATE DATABASE { site-name };
   - [x] grant user privs - GRANT ALL PRIVILEGES ON { site-name }.\* to '{
     site-name }@'localhost'
   - [x] scp dump from original
   - [x] load dump from original - cat { dumpfile }.sql | mysql -u { site-name }
     { site-name }
   - [x] update hostnames in database - see update script
 - [x] Apache
  - [x] Install - apt-get install apache2
  - [x] Configure
   - [x] a2enmod rewrite
   - [x] AllowOverride /var/wwww in apache2.conf
   - [x] Add VirtualHost in sites-available
    - [x] Route in VirtualHost tag, e.g. '\*:8080'
    - [x] DocumentRoot within VirtualHost: /var/www/{site-name}
    - [x] ErrorLog within VirtualHost: ${APACHE\_LOG\_DIR}/{site-name}-error.log
    - [x] Access log within VirtualHost: CustomLog ${APACHE\_LOG\_DIR}/{ site-name }-access.log combined
   - [x] Copy ports.conf with correct port
 - [x] PHP
  - [x] Install - apt-get install php5 php5-gd php5-mysql libapache-mod-php5
 - [x] WordPress
  - [x] mkdir /var/www/{ site-name }
  - [x] get Wordpress
   - [x] Fresh install or copy wholesale?
   - [x] Set up config vars
    - [x] DB\_NAME: { site-name }
    - [x] DB\_USER: { site-name }
    - [x] DB\_PASSWORD: { password }
    - [x] AUTH\_KEY: { random chars }
    - [x] SECURE\_AUTH\_KEY: { random chars }
    - [x] LOGGED\_IN\_KEY: { random chars }
    - [x] NONCE\_KEY: { random chars }
    - [x] AUTH\_SALT: { random chars }
    - [x] SECURE\_AUTH\_SALT: { random chars }
    - [x] LOGGED\_IN\_SALT: { random chars }
    - [x] NONCE\_SALT: { random chars }
  - [x] Copy wp-content if not already done 
