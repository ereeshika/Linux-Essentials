# Basic Nginx Setup on Ubuntu 18.04 #

## install nginx ##

```sudo apt update
sudo apt install nginx
```

## firewall-config ##

```sudo ufw allow 'Nginx HTTP'
sudo ufw status
```

## check public ip ##

```ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'
```

## setup or selcet directories ##

```sudo mkdir -p /var/www/example.com/html
```

## give access to user to edit files easily ##

```sudo chown -R $USER:$USER /var/www/example.com/html
```

## Web root permission config ##

```sudo chmod -R 755 /var/www
```

## create server block ##

```sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/example.com
sudo nano /etc/nginx/sites-available/example.com
```

### basic content of a server block ###

```server {
        listen 80;
        listen [::]:80;

        root /var/www/example.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name example.com www.example.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

## enable site bby creating a symlink ##

```sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
```

## test config for errors and restart nginx ##

```sudo nginx -t
sudo systemctl restart nginx
```

## Only if you are testing on your local machine ##

```sudo nano /etc/hosts
```

```127.0.0.1 example.com www.example.com
```