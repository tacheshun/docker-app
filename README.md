# docker-app
An example of Docker with Symfony, nginx, and MySQL

## Instructions for use

``` language-shell
git clone https://github.com/tacheshun/docker-app.git
cd docker-app

# docker user will run as www-data, a member of the www-data group
sudo chown -R $(whoami):1000 app

# bring up the environment
# this creates a ./volumes directory in the project root
make dev

# we need to sort out some permissions still, so down the environment momentarily
docker-compose down

# make the required permissions change to the php volume
sudo chown -R 1000:1000 volumes/php

# bring the environment back up
make dev

# get a terminal session open to the php container
docker-compose exec php /bin/bash
```
From here, you should be able to `composer install` ...

You will only need to do the permissions changes once. After this / subsequent development sessions, just run `make dev`.

## On Windows

``` language-shell
git clone https://github.com/tacheshun/docker-app.git
cd docker-app

composer install --no-scripts

docker-compose build --pull --no-cache 
docker-compose -f docker-compose.yml up -d --remove-orphans
```

### when you finish, don't forget to:
``` language-shell
docker-compose down 
```
