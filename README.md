# FSND Project 7 - Linux Server Configuration

##  IP, Port, URL
```
IP: 35.161.180.160 
Port: 2200  
URL:<http://ec2-35-161-180-160.us-west-2.compute.amazonaws.com/> 
``` 


## Configuration Changes

### User config:
```
useradd grader
vi /etc/sudoers.d/grader
```

### SSH Config (change port, generate key for user):
```
vi /etc/ssh/sshd_config 
ssh-keygen 
vi /root/.ssh/authorized_keys 
chmod 700 ~/.ssh
chmod 644 ~/.ssh/authorized_keys
```

### Update software:
```
sudo apt-get update
sudo apt-get upgrade
```

### Firewall Config:
```
ufw status
ufw default deny incoming
ufw default allow outgoing
ufw allow 2200/tcp
ufw allow 80/tcp
ufw allow 123
ufw enable
```

### Date config:
```
sudo dpkg-reconfigure tzdata
```

### Install packages:
```
sudo apt-get install apache
sudo apt-get install apache2
sudo apt-get install libapache2-mod-wsgi
sudo apt-get install postgresql
sudo apt-get install postgresql-server-dev-9.3
sudo apt-get install postgresql-server-dev-all
sudo apt-get install libapache2-mod-wsgi
sudo apt-get install python-pip
sudo apt-get install python-psycopg2 
sudo apt-get install postgresql postgresql-contrib
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
sudo vi flaskapp.wsgi 
sudo a2ensite FSND_Item_Catalog
sudo service apache2 reload
sudo adduser catalog
sudo su - postgres
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