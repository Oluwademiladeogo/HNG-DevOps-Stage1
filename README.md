# HNG DevOps Stage 0 - NGINX Configuration 🚀

## Overview  
This project demonstrates how to set up and configure **NGINX** on a fresh Ubuntu server to serve a custom HTML page. This task is part of **HNG DevOps Stage 0**, aimed at improving foundational web server configuration skills.

## 📌 Project Requirements  
- Install and configure **NGINX** on an Ubuntu server  
- Serve a custom HTML page as the default page  
- Ensure the webpage is accessible via the server’s public IP  

## ⚙️ Tech Stack  
- **NGINX** - Web server  
- **Ubuntu** - Operating System running on my AWS EC2 Instance  
- **Bash** - Command-line scripting  

## 🛠 Installation & Setup  

### **Step 1: Update and Install NGINX**  
Run the following commands to install and start NGINX:  
```bash
sudo apt update
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

### **Step 2: Configure the Custom HTML Page**  
Create an HTML file with the required message:  
```bash
sudo mkdir -p /var/www/html
sudo tee /var/www/html/index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DevOps Stage 0</title>
</head>
<body>
    <h1>Welcome to DevOps Stage 0 - Bickersteth Oluwademilade </h1>
</body>
</html>
EOF
```

### **Step 3: Configure NGINX**  
Modify the default NGINX config file:  
```bash
sudo nano /etc/nginx/sites-available/default
```
Update the server block to:  
```nginx
server {
    listen 80;
    server_name _;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
Save and restart NGINX:  
```bash
sudo nginx -t
sudo systemctl restart nginx
```

### **Step 4: Verify Deployment**  
Test thee setup by visiting:  
```
http://<my-server-ip>/
```
Or using:  
```bash
curl -X GET http://<my-server-ip>/
```

## 🌟 Challenges & Solutions  
**1. Firewall blocking access** → Fixed by allowing NGINX through UFW:  
```bash
sudo ufw allow 'Nginx HTTP'
sudo ufw reload
```

**2. NGINX not restarting** → Debugged with `sudo nginx -t` before restarting.  

## 📈 Learning Outcomes  
- Configuring a **basic web server**  
- Managing **firewall rules**  
- Writing a simple **NGINX configuration**  
- Deploying a static webpage  

## 🏆 Author  
[Bickersteth Oluwademilade](https://github.com/Oluwademiladeogo)  
