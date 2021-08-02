# Magento 2.4 dev environment using Docker

A docker setup for Magento2.3 development.

## Requirements

- Docker: <https://docs.docker.com/engine/installation/#supported-platforms>
- Magento2.4: You should be able to provide your own clean Magento2.4 installation. (Since this build uses PHP version 7.4 only Magento2.4 will work).

Make sure you got both Docker: `docker -v` and docker-compose: `docker-compose -v`

## Usage

1. Navigate to the root of this project.
2. Add your Magento installation and name the folder containing your Magento files as `magento`. (If you want to call it anything else please also change this on line 10 and 23 of the docker-compose.yml file).
3. Build the project with `docker-compose build`
   - Make sure you Use Linux containers (Windows only)
   - Execute commands in CMD as administrator (Windows only)
4. Start the services by using `docker-compose up` you can add the -d option to run the services in the background.
5. Use `docker container ls` to check the status of the current active containers.

```bash
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                      NAMES
56a5c7a3288c        magento24_web         "/docker-entrypoint.…"   30 minutes ago      Up 30 minutes       0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   magento-web
472557c7720a        magento24_php         "docker-php-entrypoi…"   30 minutes ago      Up 30 minutes       9000/tcp                                   magento-php
da16d6798556        elasticsearch:7.9.0   "/tini -- /usr/local…"   30 minutes ago      Up 30 minutes       0.0.0.0:9200->9200/tcp, 9300/tcp           magento-es
c2295a625dd7        mariadb:10.4          "docker-entrypoint.s…"   30 minutes ago      Up 30 minutes       0.0.0.0:3306->3306/tcp                     magento-db
```

6. You can use bash commands within a container by using `docker exec -ti <CONTAINER_NAME> bash` (CONTAINER_ID instead of CONTAINER_NAME will also work)
7. You can stop the containers by using `docker-compose stop`. Or stop a specific container by using `docker stop <CONTAINER_NAME>`
8. To access the Magento 2 shop in your browser use **https://localhost** as url. Note on MacOS the .local extension should be bypassed in the proxy settings. (Settings -> Network -> Advanced -> Proxies -> add `*.local` in the text area).
9. During the Magento installation step, use the following credentials for your Database:
   1. Database Server Host: db:3306
   2. Database Server Username: magento
   3. Database Server Password: magento
   4. Database name: magento

## SSL

Support for SSL has been added, pasting a `localhost.pem` and `localhost-key.pem` file in
the `docker/nginx/certs` folder will enable SSL for localhost out of the box. If you want to
use a different hostname or certificate name change the `docker/nginx/magento.conf` file.

## Magento CLI installation

You can use the following command to install Magento using the command line.

```bash
php bin/magento setup:install \
    --cleanup-database \
    --db-host="db:3306" \
    --db-name="magento" \
    --db-user="magento" \
    --db-password="magento" \
    --search-engine="elasticsearch7" \
    --elasticsearch-host="es" \
    --elasticsearch-port="9200" \
    --currency="EUR" \
    --timezone="Europe/Amsterdam" \
    --language="en_US" \
    --admin-user="admin" \
    --admin-password="password" \
    --admin-email="email@email.com" \
    --admin-firstname="Firstname" \
    --admin-lastname="Lastname" \
    --backend-frontname="admin"
```

## Vendor files

To speed up the environment, the vendor files in the bind mount, instead they are persisted in a named volume.
This means that the vendor files will not be synced to your local working directory. To download the vendor
files to your host machine (This is useful for autocompletion in IDE's) use the following command:

```bash
docker cp magento-php:/app/vendor ./magento/
```