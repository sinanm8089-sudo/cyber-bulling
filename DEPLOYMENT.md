# LAMP Stack Deployment Guide (Linux + Apache + MySQL + Python)

Follow these steps to deploy the Cyberbullying Detection System on an Ubuntu/Debian Linux server using Apache (`mod_wsgi`) and MySQL.

## 1. System Requirements & Packages

Connect to your Ubuntu server via SSH and install the required system packages:

```bash
sudo apt update
sudo apt install apache2 libapache2-mod-wsgi-py3 mysql-server python3-pip python3-venv pkg-config default-libmysqlclient-dev tesseract-ocr
```

## 2. Setup MySQL Database

Secure your MySQL installation and create the database:

```bash
sudo mysql_secure_installation
```

Log into MySQL as root:
```bash
sudo mysql -u root -p
```

Run the following SQL commands to create the database and user:
```sql
CREATE DATABASE cyberbullying CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'db_user'@'localhost' IDENTIFIED BY 'db_password';
GRANT ALL PRIVILEGES ON cyberbullying.* TO 'db_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
> Make sure to replace `db_user` and `db_password` with secure values!

## 3. Application Setup

Move your project files to `/var/www/cyberbullying/`.
Set up a Python virtual environment and install dependencies:

```bash
cd /var/www/cyberbullying
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Run database migrations:
```bash
export DB_ENGINE=mysql
export DB_NAME=cyberbullying
export DB_USER=db_user
export DB_PASSWORD=db_password

python manage.py migrate
```

Collect static files:
```bash
python manage.py collectstatic --noinput
```

Create a superuser for the admin dashboard:
```bash
python manage.py createsuperuser
```

## 4. Permissions

Give Apache ownership of the project files so it can serve media and static files:

```bash
sudo chown -R www-data:www-data /var/www/cyberbullying
sudo chmod -R 775 /var/www/cyberbullying/media
```

## 5. Configure Apache

Copy the provided Apache configuration file to the sites-available directory:

```bash
sudo cp /var/www/cyberbullying/apache_cyberbullying.conf /etc/apache2/sites-available/cyberbullying.conf
```

Enable the site and restart Apache:

```bash
sudo a2ensite cyberbullying.conf
sudo a2dissite 000-default.conf
sudo systemctl restart apache2
```

## 6. Verification

Navigate to your server's IP address or domain name in a web browser. The Cyberbullying system should now be running in production!
