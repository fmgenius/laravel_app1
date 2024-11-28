#  **Install Laravel on Ubuntu with Apache**

### **Prerequisites**
Ensure you have the following application installed:

1. Ubuntu 20.04/22.04 server with a non-root user account with sudo privileges.
2. Apache and properly configured on your Ubuntu server.
3. PHP installed on your Ubuntu server.
4. Composer installed on your Ubuntu server.

### Step 1: Update System Packages

```
sudo apt update
sudo apt upgrade

```
### Step 2: Install PHP and Required Extensions

```
sudo apt install php php-cli php-common php-mbstring php-xml php-zip php-mysql php-pgsql php-sqlite3 php-json php-bcmath php-gd php-tokenizer php-xmlwriter
```
Verify the PHP version after installation by running the command.

```
php -v
```
![php7.png](https://mdedit.s3.us-west-2.amazonaws.com/cb9ff36d-e025-4695-b75a-2596876af0cd.png)

### Step 3: Install Composer

```
sudo apt install curl php-cli php-mbstring git unzip
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```
Verify the installation with this command
```
composer --version
```
![composer.png](https://mdedit.s3.us-west-2.amazonaws.com/dfcf639d-1dd2-4636-9f4b-d92f40ead49e.png)

### Step 4: Install Laravel
Go to the root folder of apache which /var/www/html and run this command

```
sudo composer create-project --prefer-dist laravel/laravel genius-app
```
Once the installation is complete, navigate to the project directory:
```
cd genius-app
```
### Step 5: Configure Apache for your laravel project

```
sudo nano /etc/apache2/sites-available/genius-app.conf
```
Add the following content to the configuration file:

```
<VirtualHost *:80>
    ServerName your-domain-or-ip
    DocumentRoot /var/www/html/genius-app/public
    <Directory /var/www/html/genius-app>
        AllowOverride All
    </Directory>
</VirtualHost>
```

Replace your-domain-or-ip with your actual domain name or server IP address.

Enable the Apache rewrite module:

```
sudo a2enmod rewrite
```
Enable the virtual host:

```
sudo a2ensite genius-app.conf
```
Restart Apache for the changes to take effect:
```
sudo systemctl restart apache2
```

### Step 6: Laravel Configuration
Since we have configured our web server, the next thing is to set up laravel.
Copy the example .env file:

```
sudo cp .env.example .env
```
Generate a new application key:

```
sudo php artisan key:generate
```
Set the appropriate permissions on Laravel directories:

```
sudo chown -R www-data:www-data /var/www/html/genius-app/storage
sudo chmod -R 775 /var/www/html/genius-app/storage
```
Access your Laravel application in a web browser by visiting your domain name or server IP address.

![Screenshot 2024-11-27 at 11.21.17 PM.png](https://mdedit.s3.us-west-2.amazonaws.com/d9ea7578-7199-44f5-be7a-6fb5165de0fc.png)




