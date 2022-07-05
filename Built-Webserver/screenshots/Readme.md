# **BUILT WEB SERVER IN LOCAL SERVER** #

### 1. Clone repository from Github served by Dicoding. ###

First things first, clone repository from Dicoding's Github. <br>

    git clone https://github.com/dicodingacademy/a387-jarkom-labs.git
![Clone](clone.png) <br>

Second things, you need NodeJS to run this app. So that you have to install NodeJS along with NPM. You can use NVM tool that you learnt before. The minimum NVM version for this project is v14.15.4. <br>

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

    exec bash
    nvm install 14
![install-node](install-node.png) <br>

Third, you have to do `npm install` for installing the repository packages. <br>
![npm-i](npm-i.png) <br>

Fourth, change the node.js web server response that was originally "Hello world!" to be `your full name`. Try to run the app and open the browser. <br>
![change-content](change-content.png) <br>
![run-app](run-app.png) <br>

### 2. Install Nginx as Web Server. ###

- Not only NodeJS but also you need to install Nginx as the web server.

        sudo apt install nginx -y
    ![install-nginx](install-nginx.png) <br>

- And then you must set up the firewall. <br>
![firewall](firewall.png) <br>

- Change port nginx to be 3000. <br>

        sudo nano /etc/nginx/sites-available/default

        sudo nginx -t
        sudo systemctl reload nginx
    ![nginx-port](nginx-port.png) <br>

- Next, get the browser and input the ip address. <br>
![nginx](nginx.png) <br>

- Make a reverse proxy configuration for the app. Open the browser and check it up. <br>

        sudo nano /etc/nginx/sites-available/default
    ![config-rp](config-rp.png) <br>
    ![rep-run](rp-run.png) <br>

- Here, you can set the rate limit request. <br>

        limit_req_zone $binary_remote_addr zone=one:10m rate=6r/m;
    ![req-rate](req-rate.png) <br>
    ![temporary](temporary.png) <br>

### 3. Custom Domain and configuration SSL. ###

- Clone repository from `git@github.com:limonazzo/green-ssl-local.git`. <br>
- Run cfcfle.sh file. <br>
        sudo sh cfcfle.sh `your custom domain`

- From that command, you will get 2 files, `.crt & .key`. Copy both of them to new directory.

        sudo mkdir ssl

        cp ssl_certificate /etc/nginx/ssl/appjs.wine.xyz.crt;
        cp ssl_certificate_key /etc/nginx/ssl/appjs.wine.xyz.key;

- Now, config the reverse proxy, example; <br>
![sslconfig](sslconfig.png) <br>

- Import certificate to your browser, here I use Google Chrome. <br>
![importcert](importcert.png) <br>
![pem](pem.png) <br>

- Give a check sign for trusting a new Certificate Authority (CA). Reload your browser, here we go!. <br>
![done](done.png) <br>