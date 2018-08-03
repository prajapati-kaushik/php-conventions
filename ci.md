# CircleCI

[Read this first.](https://circleci.com/docs/2.0/configuration-reference)

## Getting started

Copy the configuration file of a specific branch, such as [networq-php](https://github.com/networq/networq-php).

## Workflows

### New repo

Use `.circleci/config.yml` and  `grumphp.yml` of [networq-php](https://github.com/networq/networq-php), change it a little to your needs. Change cached folder, configurate automatic deployment, etc.

### Add something to `grumphp.yml` in a repository

- Create a new branch
- Change `grumphp.yml` to your needs.
- Create a Pull Request.
- Make sure your build succeeds (and the new check succeeds)
- Follow up the workflow of the specific project or repository.

## Explained..

Below is an example file I used for [networq-php](https://github.com/networq/networq-php). Save this as `.circleci/config.yml` in your Project.

```
version: 2

install_composer: &install_composer
    run: |
        cd /tmp
        EXPECTED_SIGNATURE=$(curl -q https://composer.github.io/installer.sig)
        php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
        ACTUAL_SIGNATURE=$(php -r "echo hash_file('SHA384', 'composer-setup.php');")
        if [ "$EXPECTED_SIGNATURE" != "$ACTUAL_SIGNATURE" ]
        then
            >&2 echo 'ERROR: Invalid installer signature'
            rm composer-setup.php
            exit 1
        fi
        sudo php composer-setup.php --quiet --install-dir /usr/local/bin --filename composer
        RESULT=$?
        rm composer-setup.php
        exit $RESULT

jobs:
  build:
    docker:
      - image: circleci/php:7.1.5-browsers

    working_directory: ~/networq-php

    steps:
      - checkout

      - restore_cache:
          keys:
          - v1-dependencies-{{ checksum "composer.json" }}
          - v1-dependencies-

      - run:
        <<: *install_composer

      - run: composer install -n --prefer-dist

      - save_cache:
          paths:
            - ./vendor
          key: v1-dependencies-{{ checksum "composer.json" }}

      - run: ./vendor/bin/grumphp run
```

### version:

As you can see, it all begins with specifying the version of the Circle CI version. This currently is 2, maybe 3 in the future (I don't know). **Just don't use 1!.**

### install_composer

A little script to install composer. It will break when it has not been installed correctly. If you create a custom docker-image, please install composer in the image itself. It's faster **and** nicer.

### jobs/build/docker

Specify an image here. [Maybe choose one from here.](https://circleci.com/docs/2.0/circleci-images/). If you want to create a custom image, [just follow the documentation of CircleCI](https://circleci.com/docs/2.0/custom-images/#circleci-dockerfile-wizard). Also [see Docker documentation if you want to create a custom Dockerfile.](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

To build and push an image **to the public Docker Hub**:
1. `docker build . -t <name>` 
2. `docker login`
3. `docker push <name>/<name>:<version-tag>`

Follow: https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html

### jobs/build/steps/cache

To speed up, we retrieve caching and upload it after changing it. We use the checksum of `composer.json` (you can replace this whith `package.json` or `requirements.txt`, whatever the packagemanager of your platform). The checksum is being used to reduce the weight of constantly moving files (if you only use the last cache, then you don't have the cache of removed dependencies anymore).

#### Multiple cached folders

For example:

```
jobs:
  build:
    docker: ...

    ...

    steps:
      - checkout

      - restore_cache:
          keys:
          - v1-composer-{{ checksum "composer.json" }}
          - v1-npm-{{ checksum "package.json" }}
          - v1-composer-
          - v1-npm-

      ...

      - save_cache:
          paths:
            - ./vendor
          key: v1-composer-{{ checksum "composer.json" }}

      - save_cache:
          paths:
            - ./node_modules
          key: v1-npm-{{ checksum "package.json" }}

      ...
```

Make sure you use custom checksums for different packagemanagers (see difference between `- v1-composer-{{ checksum "composer.json" }}` and `- v1-npm-{{ checksum "package.json" }}`)

### jobs/build/steps

P.S.: read this: https://github.com/phpro/grumphp

Build and test the thing. I use grumphp here, you can add things to run using [grumphp](https://github.com/phpro/grumphp). It is really cool.

#### Using grumphp

For example phpunit:

```
$ composer require --dev phpunit/phpunit ^7
```

Then add configuration to `grumphp.yml`, [See how to do that here](https://github.com/phpro/grumphp/blob/master/doc/tasks.md).

##### phan/phan (example)

Install it: `composer require --dev phan/phan`

Documentation: https://github.com/phan/phan/wiki/Getting-Started#creating-a-config-file

Add this config-file as `.phan/config.php`, add [phan config to grumphp.yml](https://github.com/phpro/grumphp/blob/master/doc/tasks/phan.md).

##### phpstan/phpstan (example)

Install it: `composer require --dev phpstan/phpstan`

Documentation: https://github.com/phpstan/phpstan

[Add config to grumphp.yml](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpstan.md)

##### phpcs (example)

Install it: `composer require --dev squizlabs/php_codesniffer`

Documentation: https://github.com/squizlabs/PHP_CodeSniffer

[Add config to grumphp.yml](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpcs.md)

##### Tasks

Useful tasks to look into:

- [Composer](https://github.com/phpro/grumphp/blob/master/doc/tasks/composer.md)
- [Git Blacklist](https://github.com/phpro/grumphp/blob/master/doc/tasks/git_blacklist.md)
- [JsonLint](https://github.com/phpro/grumphp/blob/master/doc/tasks/jsonlint.md)
- [phpcs](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpcs.md)
- [PhpCpd](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpcpd.md)
- [Phan](https://github.com/phpro/grumphp/blob/master/doc/tasks/phan.md)
- [PHPLint](https://github.com/phpro/grumphp/blob/master/doc/tasks/phplint.md)
- [PhpMd](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpmd.md)
- [PHPMND](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpmnd.md)
- [PHPStan](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpstan.md)
- [PHPUnit](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpunit.md)
- [PhpVersion](https://github.com/phpro/grumphp/blob/master/doc/tasks/phpversion.md)
- [Security Checker](https://github.com/phpro/grumphp/blob/master/doc/tasks/securitychecker.md)
- [XmlLint](https://github.com/phpro/grumphp/blob/master/doc/tasks/xmllint.md)
- [YamlLint](https://github.com/phpro/grumphp/blob/master/doc/tasks/yamllint.md)

See list here: https://github.com/phpro/grumphp/blob/master/doc/tasks.md

#### Not using grumphp (please use grumphp)

But you can add things seperately as well, for example [phpunit](https://phpunit.de/manual/6.5/en/installation.html):

```
$ composer require --dev phpunit/phpunit ^7
```

Then add to steps:

```
- run: ./vendor/bin/phpunit --configuration phpunit.xml tests
```

This works for phpcs and other packages as well. They will appear in `vendor/bin`.



## Cool stuff to look into:

- [Deployment](https://circleci.com/docs/2.0/configuration-reference/#deploy)
- [Triggers and crontabs](https://circleci.com/docs/2.0/configuration-reference/#triggers)
- [grumphp](https://github.com/phpro/grumphp)
- [phpunit](https://phpunit.de)
- [Docker documentation for custom Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Custom Dockerfiles on CircleCI](https://circleci.com/docs/2.0/custom-images/#circleci-dockerfile-wizard)
- [Push Dockerfile to Public hub](https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html)