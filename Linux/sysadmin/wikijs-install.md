---
title: Wiki.js Installation
description: Wiki.js installation on a Linux/Nginx server
published: true
date: 2023-07-22T15:17:23.726Z
tags: linux, server, wiki.js
editor: markdown
dateCreated: 2020-08-06T21:27:16.094Z
---

This is a basic Node server install on Linux / Nginx on port 3000. For a Docker install, go to https://docs.requarks.io/install/docker. Thanks to my overall inexperience I could **not** for the life of me get Nginx to serve both the Docker *and* the rest of the static website.

## Basic Linux Installation

PostgreSQL is highly recommended by Wiki.js for best performance and future compatibility.
### Install PostgreSQL
```shell-session
$ sudo apt install postgresql libpq-dev postgresql-client postgresql-client-common
```

### Install Wiki.js
```shell-session
$ sudo mkdir /var/wiki;
cd /var/wiki;
sudo wget https://github.com/Requarks/wiki/releases/download/2.4.107/wiki-js.tar.gz;   
sudo tar xzf /var/wiki/wiki-js.tar.gz -C /var/wiki
```

### Rename default config file and modify
```shell-session
$ sudo mv /var/wiki/config.sample.yml /var/wiki/config.yml;
sudo vim /var/wiki/config.yml
```

config.yml:
```yaml
# Database
port: 3000
db:
	type: postgres
  host: localhost
  port: 5432
  user: wikijs
  pass: <db_password>
  db: wiki
  ssl: false
 
# SSL/TLS Settings
ssl:
	enabled: true
  port: 3443
  provider: letsencrypt
  domain: wiki.phiz.io
  subscriberEmail: <my@email.com>
```

### Set up PostgreSQL database

Create database user `wikijs` and enter a password (same as <db_password> in the config.yml):
```shell-session
$ sudo su postgres
createuser --pwprompt wikijs
```

Create the database and exit postgres user:
```shell
createdb -O wikijs wiki
exit
```

## Nginx reverse proxy to the subdomain

Create a `wiki.phiz.io` file entry in `/etc/nginx/sites-available/`:
```nginx
server {
    server_name  wiki.phiz.io;

    location / {
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

Symlink to sites-enabled:
```shell-session
$ sudo ln -s /etc/nginx/sites-available/wiki.phiz.io /etc/nginx/sites-enabled/wiki.phiz.io
```

Reload Nginx:
```shell-session
$ service nginx restart
```

Finally, if you haven't already, add an **A record** to your DNS panel for the subdomain, pointing to the server host IP address.
<br />

### Set up SSL certificate
Use Certbot to generate a certificate. Choose option 2 to always redirect http to https.
```shell-session
$ sudo certbot --nginx -d wiki.phiz.io
```
<br />

## Start the Wiki.js server

The server can be started simply with `node server` from `/var/www/phiz.io`. It's a good idea to use this first to test for any errors. If EACCES errors are encountered, use sudo.

For long-term deployment it should be run as a service or with a process manager such as [pm2](/Linux/sysadmin/pm2):
```shell-session
$ pm2 start server --name wiki
$ pm2 save
$ pm2 startup  # creates a startup script to auto-start server on system boot
```

Wiki.js should now be accessible at https://wiki.phiz.io!
<br />

## References
- [Linux | Wiki.js Docs *Official guide for installation, which does not include instructions for PostgreSQL setup*](https://docs.requarks.io/install/linux)
- [Configuration | Wiki.js Docs *Official configuration file info*](https://docs.requarks.io/install/config)
- [Simple PostgreSQL setup for Wiki.js? *Excxellent answer by /u/chronos280 describing basic Wiki.js setup with PostgreSQL*](https://www.reddit.com/r/selfhosted/comments/hhmec4/simple_postgresql_setup_for_wikijs/fwdqi8t/)
{.links-list}