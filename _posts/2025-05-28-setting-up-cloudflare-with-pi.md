---
layout: post
title: "Hosting Nextcloud on Raspberry Pi with Cloudflare Tunnel and Custom Domain"
author: goutham
image: https://monetize.info/wp-content/uploads/2021/05/How-to-Buy-a-Website.png
featured: true
---

If you're looking to self-host your cloud storage securely and access it anywhere in the world without opening any ports on your home router, this guide walks you through hosting Nextcloud on a Raspberry Pi, exposing it to the internet via Cloudflare Tunnel, and securing it with a custom domain.
I know the title and first line sounded overcomplicated, but it's simple and straight forward.

Before going into setup - why would one want to do this?
1. **Privacy**: Keep your data private and under your control.
2. **Accessibility**: Access your files from anywhere without relying on third-party services.
3. Most of the ISP's don't keep their ports open and buying a static IP is an additional cost + control on your data.

now, let's dig into setup part : 

Assuming you have already these components from our previous posts: 
- Nextcloud installed on Raspberry Pi
- Apache running on port 8080 (if you are only using apache without nginx - you can keep it running in port 80)
- NGINX reverse proxy for SSL (optional)
- Custom domain: <your Domain Name> 

## Coming to setup : 

### Prepare Raspberry Pi
Update system:
``
sudo apt update && sudo apt upgrade
``

Set Apache to listen on port 8080:

``bash
sudo nano /etc/apache2/ports.conf
Listen 8080

<VirtualHost *:8080> // change port here
DocumentRoot /srv/www/apache/ // change path - if your apache is configured in a different path 
...
</VirtualHost>
``

### Setup Cloudflare

- Update nameservers in your domain registrar to point to Cloudflare's nameservers. cloudflare will guide you through this process.
- Login to [cloudflare dashboard](https://dash.cloudflare.com/login) and add your domain name
- follow on screen instructions 

### Cloudflare Tunnel Configuration

Install cloudflared in pi:
``bash
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-arm64.deb
sudo dpkg -i cloudflared-linux-arm64.deb
``
Authenticate and create tunnel:
``bash
cloudflared tunnel login
cloudflared tunnel create <domain-name>-tunnel
``
Replace `<domain-name>` with your actual domain name.

Create a config file /etc/cloudflared/config.yml:

``
tunnel: pixsee-tunnel
credentials-file: /etc/cloudflared/<TUNNEL_ID>.json

ingress:
- hostname: <your Domain Name> 
  service: http://localhost:8080

- service: http_status:404
``
- Replace `<TUNNEL_ID>` with the ID from the tunnel you created.

``
sudo cloudflared --config /etc/cloudflared/config.yml tunnel run
``

sudo systemctl daemon-reload
sudo systemctl enable cloudflared
sudo systemctl start cloudflared

### Nextcloud Configuration

Update config.php:

``bash
'trusted_domains' => [
'localhost',
'192.168.1.210',
'<your Domain Name> '
],
'overwrite.cli.url' => 'https://<your Domain Name> ',
'overwritehost' => '<your Domain Name> ',
'overwriteprotocol' => 'https',
``


🎉 You're Done!

You can now access your Nextcloud securely from anywhere via https://<your Domain Name> , with no ports forwarded on your home router. The Cloudflare Tunnel ensures privacy, reliability, and dynamic IP compatibility.

