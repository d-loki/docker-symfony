docker-symfony
==============

This is a complete stack for running Symfony 5 (latest version), PHP7 using docker-compose tool.

# Installation

First, clone this repository:

```bash
$ git clone https://github.com/d-loki/docker-symfony.git
```

Next, put your Symfony application into `symfony` folder and do not forget to add `symfony.localhost` in your `/etc/hosts` file.

Make sure you adjust `database_host` in `parameters.yml` to the database container alias "db" (for Symfony < 4)
Make sure you adjust `DATABASE_URL` in `env` to the database container alias "db" (for Symfony >= 4)

Then, run:

```bash
$ docker-compose up
```

You are done, you can visit your Symfony application on the following URL: `http://symfony.localhost` (and access Kibana on `http://symfony.localhost:81`)

_Note :_ you can rebuild all Docker images by running:

```bash
$ docker-compose build
```

# How it works?

Here are the `docker-compose` built images:

* `db`: This is the MySQL database container (can be changed to postgresql or whatever in `docker-compose.yml` file),
* `php`: This is the PHP-FPM container including the application volume mounted on,
* `nginx`: This is the Nginx webserver container in which php volumes are mounted too,

This results in the following running containers:

```bash
> $ docker-compose ps
             Name                           Command               State                 Ports
-----------------------------------------------------------------------------------------------------------
mysql                            docker-entrypoint.sh --def ...   Up      0.0.0.0:3306->3306/tcp, 33060/tcp
nginx                            nginx                            Up      443/tcp, 0.0.0.0:80->80/tcp
php-fpm                          php-fpm7 -F                      Up      0.0.0.0:9000->9001/tcp
```

# Environment Customizations

You can customize the exposed ports and other parameters changing the docker-compose .env file.

# Read logs

You can access Nginx and Symfony application logs in the following directories on your host machine:

* `logs/nginx`
* `logs/symfony`

# Code license

You are free to use the code in this repository under the terms of the 0-clause BSD license. LICENSE contains a copy of this license.
