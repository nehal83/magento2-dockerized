# Dockerize Magento 2

A composer package for dockerizing Magento 2

The composer package **tddwizard/magento2-dockerized** deploys docker infrastructure defintion files such as [docker-compose.yml](docker-compose.yml) to your Magento 2 root folder and enables you to host your Magento 2 shops without having to install Apache/Nginx, MySQL or PHP on your system.

## Package Name

 `tddwizard/magento2-dockerized` (fork of `arvatoscm/dockerize-magento2`)

## Software Requirements

For Linux users you must have a recent version of [docker](https://github.com/docker/docker/releases) and [docker-compose](https://github.com/docker/compose/releases) installed.

If you are a Mac or Windows user, use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox).

## Installation

Add `tddwizard/magento2-dockerized` to your existing Magento 2 shop:

```bash
composer require --ignore-platform-reqs tddwizard/magento2-dockerized
chmod +x bin/console
```

This will place some files in your Magento root:

- `docker-compose.yml`
The docker infrastructure definition
- `bin/console`
A utility script for controlling dockerized Magento projects
- `config`
A folder which contains the configuration files for PHP, Nginx and phpMyAdmin


## Usage

`dockerize-magento2` comes with `bin/console` script that can be used to install Magento and to execute Magentos' bin/magento script inside the PHP docker container:

Trigger the Magento 2 installation process:

```bash
bin/console install <hostname>
```

Start the docker containers:

```bash
bin/console start
```

Stop the docker containers:

```bash
bin/console stop
```

Execute `bin/magento` inside the docker container:

```bash
bin/console exec [arguments]
```

For more information on how to use docker-compose visit: https://docs.docker.com/compose/

## Configuration

The `install` action depends on some parameters such as usernames and passwords. We have put in some default values for you that will work for a quick test:

```
DATABASE_NAME="magento2dockerized"
DATABASE_USER="magento"
DATABASE_PASSWORD="enAVINa2"
DATABASE_ROOT_PASSWORD="enAVINa2"

ADMIN_USERNAME="admin"
ADMIN_FIRSTNAME="Admin"
ADMIN_LASTNAME="Inistrator"
ADMIN_EMAIL="johndoe@example.com"
ADMIN_PASSWORD="enAVINa2"

DEFAULT_LANGUAGE="en_US"
DEFAULT_CURRENCY="EUR"
DEFAULT_TIMEZONE="Europe/Berlin"

BACKEND_FRONTNAME="management"
```

If you want to use different parameters change the values in the [.env](.env) file to your needs.
After customizing the parameters just run trigger the installation with `bin/console install <hostname>`.

## Integration Tests

### Setup 
1. Create database `magento_integration_tests` (easiest way is to open phpmyadmin at [http://dockerized-magento.local:8080/](http://dockerized-magento.local:8080/) and login as root)
2. Copy `magento/dev/tests/integration/etc/install-config-mysql.php.dist` to `magento/dev/tests/integration/etc/install-config-mysql.php`
3. Change database parameters in `magento/dev/tests/integration/etc/install-config-mysql.php`:

        'db-host' => 'mysql',
        'db-user' => 'root',
        'db-password' => 'enAVINa2',
        'db-name' => 'magento_integration_tests',
        'db-prefix' => '',

### Running Tests

After the integration test container is set up as described above, you can run the tests with this command:

    docker-compose -f docker-compose.yml -f docker-compose.integration-tests.yml run --rm integration

## Licensing

dockerize-magento2 is licensed under the Apache License, Version 2.0.
See [LICENSE](LICENSE) for the full license text.
