## apache

## mysql

We've installed your MySQL database without a root password. To secure it run:
    mysql_secure_installation

To connect run:
    mysql -uroot

To have launchd start mysql now and restart at login:
  brew services start mysql
Or, if you don't want/need a background service you can just run:
  mysql.server start
  
- 帳密 
	- root
	- null

## php

php.ini : `/usr/local/etc/php/{version}/php.ini`