---
layout: post
title: "Simple deployment to nginx using rsync"
date: 2013-01-19 21:33
comments: true
categories: 
---

I'm hosting my websites on a small virtual server from Hetzner.

The setup with nginx was surprisingly simple after I found the right guides :)

I like to have all configs and data contained in one directory so that I can edit everything offline and just rsync it with the server.
{more}
##Local machine setup
Create a folder structure like this:

```
www
|-- sites-available
+-- sites-enabled
    +-- domains
        +-- yourdomain.com
```

The sites-available folder will contain a config file per domain:

```
# www/sites-available/yourdomain.com

server {
  listen  80;
  server_name .yourdomain.com;
  root /home/your_user/www/domains/yourdomain.com;
  index index.html;
}
```

To enable a domain you now just symlink the domain's config into sites-enabled:
```
cd www/sites-enabled
ln -s ../sites-available/yourdomain.com yourdomain.com
```
Its important that your symlinks are relative otherwise they will break on the server!

Create the folder from where yourdomain.com gets served:
```
cd www/domains
mkdir yourdomain.com
echo "Hello world!" >> yourdomain.com/index.html
```

Rsync everything to your server:
```
rsync -avzr --delete --force www/ your_user@$your_ip:
```

##Server setup

I'm using Ubuntu Server 12.10.

SSH into your server - all following commonds need sudo rights:
```
ssh your_user@your_ip
```

Install nginx:
```
apt-get install nginx
```

We symlink nginx's sites-enabled folder to the one in our home folder:

```
rm -r /etc/nginx/sites-enabled

ln -s /home/your_user/www/sites-enabled /etc/nginx/sites-enabled
```

Restart nginx:
```
service nginx restart
```

Everything should be running :)

You can now simply update your sites on your local machine and only need to run rsync to deploy.  
Note: Everytime you edit your configs or the sites-enabled folder you need to restart nginx again.

