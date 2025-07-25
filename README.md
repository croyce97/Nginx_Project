

# Nginx Project



##  Overview

I deployed a full-stack PERN (PostgreSQL, Express, React, Node.js) application using Nginx as a reverse proxy. SSL was configured with a valid certificate to enable secure HTTPS access.

##  Setup Instructions
```
git clone https://github.com/croyce97/Nginx_Project
cd Nginx_Project
sudo apt update
sudo apt install npm
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs

sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql
sudo -u postgres psql
ALTER USER postgres WITH PASSWORD 'postgres';
\q
sudo -u postgres psql -f server/database.sql

cd server
npm install

cd ../client
npm install
npm run build
```
* Configured Nginx as a reverse proxy with SSL support using a self-signed certificate
```
sudo mkdir /etc/nginx/ssl/pern_app_ssl
cd /etc/nginx/ssl/pern_app_ssl/

sudo openssl req -x509 -nodes -days 365 \
-newkey rsa:2048 \
-keyout canhnq.com.key \
-out canhnq.com.crt \
-subj "/C=VN/ST=Hanoi/L=Hanoi/O=LocalOrg/OU=IT/CN=canhnq.com"
```
Copy [pern-app](https://github.com/croyce97/Nginx_Project/blob/main/nginx-pern-app.cfg) into `pern-app`.
```
sudo vi /etc/nginx/sites-available/pern-app
sudo ln -sf /etc/nginx/sites-available/pern-app /etc/nginx/sites-enabled/pern-app
sudo nginx -t

node index.js
sudo systemctl reload nginx

```


Local Windows Machine: 
+ Open Notepad as Administrator
+ Open the file: `C:\Windows\System32\drivers\etc\hosts`
+ Add: `192.168.232.110    canhnq`

Visit: `canhnq.com` or `192.168.232.110:80` [https://canhnq.com](https://github.com/croyce97/Nginx_Project/blob/main/canhnq-https.jpeg)
