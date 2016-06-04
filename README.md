# docker-compose-wordpress-nginx
Using docker compose to launch wordpress with nginx and php-fpm.

In the repository, three ways to build wordpress.

*docker-wordpress-1*: Using official images to run wordpress.

*docker-wordpress-2*: Build the chinese version wordpress then run.

*docker-wordpress-3*: Separate php-fpm and wordpress, need to provide wordpress source files yourself.

## Installation

Clone the repository or download zip and decompression.

```bash
$ git clone https://github.com/mzsea/docker-compose-wordpress-nginx.git
```

## Usage

Before run, you can modify profiles with your parameters.

e.g. official image version, ports, mysql password, wordpress version.

* If use *docker-wordpress-2*, don't forget to check the execute permission of  `docker-entrypoint.sh`, if it don't has, change using :

    ```bash
    $ chmod 755 docker-entrypoint.sh
    ```

* If use *docker-wordpress-3*, download wordpress from official website and decompress source files to *wordpress* folder.Note that, when docker containers started, there is still something to do, see underside.

The `docker-compose.yml` file using the version 2 syntax, and version 2 files are supported by Compose 1.6.0+ and require a Docker Engine of version 1.10.0+.

Final, execute the following command:

```bash
$ docker-compose up -d
```

When started, if use *docker-wordpress-3*, do next:

1. Create database for wordpress:
    ```bash
    $ docker exec -it <mysql_container_name> bash
    root@e50ef7ccca8f:/# mysql -u root -p
    Enter password: your_password
    mysql> CREATE DATABASE IF NOT EXISTS `wordpress`;
    mysql> eixt;
    root@e50ef7ccca8f:/# eixt
    ```
2. Change permissions of wordpress source files:
    ```bash
    $ docker exec -it <php_container_name> bash
    root@867b00000e95:/var/www/html# cd ..
    root@867b00000e95:/var/www# chown -R www-data:www-data html
    root@867b00000e95:/var/www# exit;
    ```

Then, you can configure wordpress via URL in a browser and enjoy it.
