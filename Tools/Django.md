sudo apt install -y apache2 libapache2-mod-wsgi-py3

sudo systemctl enable --now apache2 && sudo systemctl status apache2


sudo apt install -y mysql-server libmysqlclient-dev pkg-config

sudo systemctl enable --now mysql && sudo systemctl status mysql

sudo mysql -u root

CREATE DATABASE itam_db;
CREATE USER 'itam_user'@'localhost' IDENTIFIED BY '817934';
GRANT ALL ON itam_db.* TO 'itam_user'@'localhost';
FLUSH PRIVILEGES;
EXIT

python3 -V
sudo apt install -y python3-venv python3-pip
pip3 --version

mkdir /var/www/fyp_project
sudo chown -R $USER:$USER /var/www/fyp_project 
cd /var/www/fyp_project

python3 -m venv django_env
source django_env/bin/activate

pip3 install django
django-admin --version

pip3 install mysqlclient

django-admin startproject itam_app .
nano itam_app/settings.py

ALLOWED_HOSTS = ['192.168.31.134']

DATABASES = {
	'default': {
	'ENGINE': 'django.db.backends.mysql',
	'NAME': 'itam_db',
	'USER': 'itam_user',
	'PASSWORD': '817934',
	'HOST': '127.0.0.1',
	'PORT' : '3306',
	}
}



STATIC_URL='/static/'

import os
STATIC_ROOT=os.path.join(BASE_DIR, 'static/') 
MEDIA_URL='/media/'
MEDIA_ROOT=os.path.join(BASE_DIR, 'media/')

./manage.py  makemigrations
./manage.py  migrate
./manage.py createsuperuser
./manage.py collectstatic
deactivate


nano /etc/apache2/sites-available/django.conf

<VirtualHost *:80>

        ServerAdmin admin@liqing.com
        ServerName liqing.com
        ServerAlias www.liqing.com

        DocumentRoot /var/www/fyp_project/

        ErrorLog ${APACHE_LOG_DIR}/liqing.com_error.log
        CustomLog ${APACHE_LOG_DIR}/liqing.com_access.log combined

        Alias /static /var/www/fyp_project/static
        <Directory /var/www/fyp_project/static>
                Require all granted
        </Directory>

        Alias /media /var/www/fyp_project/media
        <Directory /var/www/fyp_project/media>
                Require all granted
         </Directory>

        <Directory /var/www/fyp_project/itam_app>
                <Files wsgi.py>
                        Require all granted
                </Files>
        </Directory>

        WSGIDaemonProcess itam_app python-path=/var/www/fyp_project python-home=/var/www/fyp_project/django_env
        WSGIProcessGroup itam_app
        WSGIScriptAlias / /var/www/fyp_project/itam_app/wsgi.py

</VirtualHost>

sudo a2ensite liqing.com.conf
sudo a2dissite 000-default.conf
sudo systemctl restart apache2
