# Magento 2.3 dev environment using Docker

A docker setup for Magento2.3 development.

## Requirements

- Docker: <https://docs.docker.com/engine/installation/#supported-platforms>
- Magento2.3: You should be able to provide your own clean Magento2.3 installation. (Since this build uses PHP version 7.2 only Magento2.3 will work).

Make sure you got both Docker: `docker -v` and docker-compose: `docker-compose -v`

## Usage

1. Navigate to the root of this project.
2. Add your Magento installation and name the folder containing your Magento files as `Magento`. (If you want to call it anything else please also change this on line 7 and 19 of the docker-compose.yml file).
3. Build the project with `docker-compose build`
    - Make sure you Use Linux containers (Windows only)
    - Execute commands in CMD as administrator (Windows only)
4. Start the services by using `docker-compose up` you can add the -d option to run the services in the background.
5. Use `docker ps` to check the status of the current active containers.

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
21028c6d2596        nginx:1.13          "nginx -g 'daemon ..."   28 minutes ago      Up 4 seconds        0.0.0.0:80->80/tcp       magento2_web_1
28c2f2f275b9        magento2_php        "docker-php-entryp..."   28 minutes ago      Up 5 seconds        9000/tcp                 magento2_php_1
70c22e0cc9cd        mysql:5.7           "docker-entrypoint..."   About an hour ago   Up 6 seconds        0.0.0.0:3306->3306/tcp   magento2_db_1
```

5. You can use bash commands within a container by using `docker exec -ti <CONTAINER_NAME> bash` (CONTAINER\_ID instead of CONTAINER\_NAME will also work)
6. You can stop the containers by using `docker-compose stop`. Or stop a specific container by using `docker stop <CONTAINER_NAME>`
7. To access the Magento 2 shop in your browser use  **magento2-dev.local** as url. Note on MacOS the .local extension should be bypassed in the proxy settings. (Settings -> Network -> Advanced -> Proxies -> add `*.local` in the text area).
8. During the Magento installation step, use the following credentials for your Database:
   1. Database Server Host: db:3306
   2. Database Server Username: magento
   3. Database Server Password: magento
   4. Database name: magento
