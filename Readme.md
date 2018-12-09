# OpenCart Docker Orchestration

[OpenCart](https://www.opencart.com/) - The best FREE and open-source eCommerce platform

## Install

    $ git clone https://github.com/avoinea/docker.deploy.opencart mystore.com
    $ cd mystore.com
    $ cp .env.example .env
    $ vim .env

## SSL certificates

* Obtain your SSL certificates from letsencrypt

      $ docker run --rm \
                   -p 80:80 \
                   -p 443:443 \
                   -v certs:/etc/letsencrypt \
               certbot/certbot certonly --standalone

* If you already have SSL certificates

      $ docker run -it --rm -v certs:/etc/letsencrypt -v /path/my/certs:/backup alpine sh
      $ mkdir -p /etc/letsencrypt/live/www.myblog.com/
      $ cd /backup
      $ cp cert.pem privkey.pem fullchain.pem /etc/letsencrypt/live/www.myblog.com/
      $ exit

## Run

    $ docker-compose pull
    $ docker-compose up -d

## Customize your store

    https://www.mystore.com/admin

## Renew SSL certificates

### First run:

      $ docker-compose stop
      $ docker run --name=letsentrypt \
                   -p 80:80 \
                   -p 443:443 \
                   -v certs:/etc/letsencrypt \
               certbot/certbot renew
      $ docker-compose up -d

### Next run:

      $ docker-compose stop
      $ docker start letsencrypt
      $ docker-compose up -d

