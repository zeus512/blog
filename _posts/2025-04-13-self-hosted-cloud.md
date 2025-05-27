---
layout: post
title: "Self-Hosted Cloud: Installing Nextcloud on Raspberry Pi"
author: goutham
tags: [Nextcloud, Raspberry Pi, Cloud Storage, Self-Hosted, Linux]
featured: false
---

Want your own private Google Drive or Dropbox? With **Nextcloud** and a **Raspberry Pi**, you can host your own cloud storage, accessible across your local network. 🏠☁️

In this post, we’ll walk through installing **Nextcloud** on a **Raspberry Pi 3** from scratch — including PHP, database, web server, and self-signed HTTPS.

---

## 🧰 Prerequisites

- Raspberry Pi 3 (or newer) running Raspberry Pi OS
- Internet connection (Wi-Fi or Ethernet)
- MicroSD card (16GB+)
- Optional: External USB storage
- SSH access or connected keyboard and screen

---

## 🔧 Step 1: Update System

```bash
sudo apt update && sudo apt upgrade -y
```
Common Errors:
```
dpkg was interrupted: Fix with
```

```bash
sudo dpkg --configure -a
```

## 🌐 Step 2: Install Nginx, PHP, and MySQL
We’ll be using Nginx as a lightweight and fast web server.

```bash
sudo apt install nginx php-fpm php-mysql mariadb-server unzip curl -y
```

Additional PHP modules needed by Nextcloud:

```bash
sudo apt install php-curl php-gd php-xml php-zip php-mbstring php-bz2 php-intl php-bcmath php-gmp php-imagick -y
```

## 🛠️ Step 3: Configure MariaDB (MySQL)

```bash
sudo mysql_secure_installation
```
Choose a strong root password, and answer the prompts as:
Remove anonymous users: Yes
Disallow root login remotely: Yes
Remove test database: Yes
Then create the Nextcloud DB:

```bash
sudo mysql -u root -p
```
Inside MySQL prompt:


```
CREATE DATABASE nextcloud;
CREATE USER 'nextclouduser'@'localhost' IDENTIFIED BY 'your-password';
GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextclouduser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## 📦 Step 4: Download & Extract Nextcloud

```bash

cd /var/www/
sudo curl -O https://download.nextcloud.com/server/releases/latest.zip
sudo unzip latest.zip
sudo chown -R www-data:www-data nextcloud
sudo chmod -R 755 nextcloud
```

## 🌐 Step 5: Configure Nginx
Create a new config file:

```bash
sudo nano /etc/nginx/sites-available/nextcloud
```
Paste the config:

```
server {
    listen 443 ssl;
    server_name 192.168.1.210;

    ssl_certificate /etc/ssl/certs/nextcloud.crt;
    ssl_certificate_key /etc/ssl/private/nextcloud.key;

    root /var/www/nextcloud;
    index index.php index.html;

    location / {
        try_files $uri $uri/ /index.php$request_uri;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

Enable the config:

```bash

sudo ln -s /etc/nginx/sites-available/nextcloud /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

## 🔐 Step 6: Create Self-Signed HTTPS Cert
```bash

sudo openssl req -x509 -nodes -days 365 \
-newkey rsa:2048 -keyout /etc/ssl/private/nextcloud.key \
-out /etc/ssl/certs/nextcloud.crt
```
Use your own name/email/org when prompted. It’s just for internal encryption.

## 🚀 Step 7: Access Nextcloud Web Installer
Go to:

```
https://192.168.1.210
```
⚠️ You’ll see a browser warning due to the self-signed cert. Accept it and continue.

Create admin user

Use database:

DB user: nextclouduser

Password: your-password

DB name: nextcloud

Host: localhost

## 🧪 Troubleshooting Tips
<div class="datatable-begin"></div>

| Issue                   | Fix                                                                      |
|-------------------------|--------------------------------------------------------------------------|
| 403 Forbidden           | Ensure permissions: `sudo chown -R www-data:www-data /var/www/nextcloud` |
| File not found          | Check Nginx root path matches: `root /var/www/nextcloud;`                |
| Can't connect to DB     | Confirm user/pass/db name are correct in the web form                    |
| Self-signed SSL warning | This is expected; use Let's Encrypt later for real cert                  |

<div class="datatable-end"></div>


## ✅ Final Thoughts
At this stage, your Raspberry Pi is now acting as a personal Nextcloud server. 🎉

In the next post, we’ll tackle static IPs, router configuration, and hostname issues for reliable access.

Stay tuned!

yaml


---
