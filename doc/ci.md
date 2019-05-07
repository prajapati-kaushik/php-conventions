# CircleCI

[Read this first.](https://circleci.com/docs/2.0/configuration-reference)

See also [GrumPHP](grumphp.md)

## Getting started

Copy the configuration file of a specific branch, such as [networq-php](https://github.com/networq/networq-php).

## Workflows

### New repository

Use `doc/.circleci/config.yml` for CI installation. Change it a little to your needs. Change cached folder, configurate automatic deployment, etc.

### Add something to `grumphp.yml` in a repository

- Create a new branch
- Change `grumphp.yml` to your needs.
- Create a Pull Request.
- Make sure your build succeeds (and the new check succeeds)
- Follow up the workflow of the specific project or repository.

## Explained..

See `doc/.circleci/config.yml`, save this as `.circleci/config.yml` in your project.

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

To speed up, we retrieve caching and upload it after changing it. We use the checksum of `composer.json` (you can replace this with `package.json` or `requirements.txt`, whatever the package manager of your platform). The checksum is being used to reduce the weight of constantly moving files (if you only use the last cache, then you don't have the cache of removed dependencies anymore).

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

Make sure you use custom checksums for different package managers (see difference between `- v1-composer-{{ checksum "composer.json" }}` and `- v1-npm-{{ checksum "package.json" }}`)

### jobs/build/steps

P.S.: read this: https://github.com/phpro/grumphp

Build and test the thing. I use grumphp here, you can add things to run using [grumphp](https://github.com/phpro/grumphp). It is really cool.

## Cool stuff to look into:

- [Deployment](https://circleci.com/docs/2.0/configuration-reference/#deploy)
- [Triggers and crontab](https://circleci.com/docs/2.0/configuration-reference/#triggers)
- [grumphp](https://github.com/phpro/grumphp)
- [phpunit](https://phpunit.de)
- [Docker documentation for custom Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Custom Dockerfiles on CircleCI](https://circleci.com/docs/2.0/custom-images/#circleci-dockerfile-wizard)
- [Push Dockerfile to Public hub](https://ropenscilabs.github.io/r-docker-tutorial/04-Dockerhub.html)
