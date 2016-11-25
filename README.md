# FSND Project 7 - Linux Server Configuration

##  IP, Port, URL
```
IP: 35.164.114.224
Port: 2200  
URL: http://ec2-35-164-114-224.us-west-2.compute.amazonaws.com/ 
``` 


## Configuration Changes

### User config:
```
useradd -m grader
vi /etc/sudoers.d/grader  # (add "grader ALL=(ALL) NOPASSWD:ALL" to this file)
```

### SSH Config (change port, generate key for user):
```
vi /etc/ssh/sshd_config  # (change port)
service ssh restart

ssh-keygen 
vi /root/.ssh/authorized_kcat eys 
chmod 700 ~/.ssh
cat .ssh/id_rsa.pub >> .ssh/authorized_keys
chmod 644 ~/.ssh/authorized_keys
```

### Update software:
```
sudo apt-get update
sudo apt-get upgrade
```

### Firewall Config:
```
sudo ufw status
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2200/tcp
sudo ufw allow 80/tcp
sudo ufw allow 123
sudo ufw enable
```

### Date config:
```
sudo dpkg-reconfigure tzdata
```

### Install packages:
```
sudo apt-get install apache2 libapache2-mod-wsgi
sudo apt-get install postgresql postgresql-server-dev-9.3 postgresql-server-dev-all postgresql-contrib
sudo apt-get install python-pip python-psycopg2 git
sudo pip install virtualenv
sudo pip install Flask 
sudo pip install bleach
sudo pip install oauth2client
sudo pip install requests
sudo pip install httplib2
sudo pip install flask-httpauth
sudo pip install redis
sudo pip install oauth2client
sudo pip install sqlalchemy
```

### Clone Git repository:
```
sudo git clone https://github.com/TrueZarathustra/FSND_Item_Catalog.git
sudo touch .htaccess
sudo vi .htaccess
``` 

### Configure Apache, Postgresql:
```
sudo vi /etc/apache2/sites-available/FSND_Item_Catalog.conf
```

configure flaskapp.wsgi:
```
sudo vi flaskapp.wsgi 
# Add:
#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/FSND_Item_Catalog/")
from project import app as application
application.secret_key = 'super_secret_key'
```

configure FSDN_Item_Catalog.conf:
```
sudo vi /etc/apache2/sites-available/FSND_Item_Catalog.conf
#Add:
<VirtualHost *:80>
        ServerName 52.34.247.81
        ServerAdmin admin@mywebsite.com
        WSGIScriptAlias / /var/www/FSND_Item_Catalog/flaskapp.wsgi
        <Directory /var/www/FSND_Item_Catalog/>
            Order allow,deny
            Allow from all
        </Directory>
        Alias /static /var/www/FSND_Item_Catalog/static
        <Directory /var/www/FSND_Item_Catalog/static/>
            Order allow,deny
            Allow from all
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/error.log
        LogLevel warn
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Apply changes:
```
sudo a2ensite FSND_Item_Catalog
sudo service apache2 reload
```

Configure DB:
```
sudo adduser catalog
sudo su - postgres
psql

CREATE ROLE catalog WITH CREATEDB;
ALTER ROLE catalog WITH PASSWORD 'qwerty';
ALTER ROLE catalog LOGIN;
CREATE DATABASE catalog WITH OWNER catalog;
\c catalog
REVOKE ALL ON SCHEMA public FROM public;
GRANT ALL ON SCHEMA public TO catalog;
```

### Fix python code (change path to client_secrets.json, DB_connection, etc):
```
sudo vi database_setup.py
sudo vi project.py
sudo vi lotsofbooks.py
sudo python lotsofbooks.py
sudo python database_setup.py
```

### URLs:
```
http://stackoverflow.com/questions/67631/how-to-import-a-module-given-the-full-path
http://ru.stackoverflow.com/questions/140785/%D0%9A%D0%B0%D0%BA-%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%B8%D1%82%D1%8C-%D0%BF%D1%83%D1%82%D1%8C-%D0%B2-%D0%BF%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%83%D1%8E-path
http://stackoverflow.com/questions/5841531/django-mod-wsgi-apache-importerror-at-no-module-named-djproj-urls
https://www.postgresql.org/docs/9.0/static/sql-alterrole.html
https://www.postgresql.org/docs/9.3/static/sql-dropuser.html
https://discussions.udacity.com/t/cant-find-image/43142/4
https://discussions.udacity.com/t/cant-find-image/43142/2
https://serversforhackers.com/configuring-apache-virtual-hosts
http://dev.mysql.com/doc/refman/5.7/en/alter-user.html
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
https://help.ubuntu.com/community/AptGet/Howto#Maintenance_commands
https://www.cyberciti.biz/faq/howto-add-postgresql-user-account/
https://www.cyberciti.biz/tips/postgres-allow-remote-access-tcp-connection.html
http://askubuntu.com/questions/138423/how-do-i-change-my-timezone-to-utc-gmt
https://help.ubuntu.com/community/UFW
http://debian-help.ru/articles/ustanovka-i-nastroika-sudo-v-debian-7/#config
http://debian-help.ru/articles/ustanovka-i-nastroika-sudo-v-debian-7/
http://wiki.russianfedora.pro/index.php?title=%D0%9A%D0%B0%D0%BA_%D1%80%D0%B0%D0%B7%D1%80%D0%B5%D1%88%D0%B8%D1%82%D1%8C_%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF_%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8E_%D0%BA_%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B5_sudo%3F
https://aws.amazon.com/ru/sdk-for-python/
https://linux.die.net/man/1/ssh-keygen
https://www.opennet.ru/cgi-bin/opennet/man.cgi?topic=ssh-keygen&category=1
http://unix.stackexchange.com/questions/36072/how-to-expire-a-password-for-inital-account-creation
http://superuser.com/questions/626843/does-the-root-account-always-have-uid-gid-0
```
