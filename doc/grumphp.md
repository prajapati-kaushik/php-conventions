## GrumPHP

We're using [GrumPHP](https://github.com/phpro/grumphp) to automatically check for code-quality.

#### GrumPHP install and use

1. Install packages under require-dev section in your `composer.json` file.

```json
    "require-dev": {
          "phpro/grumphp": "^0.14",
          "sebastian/phpcpd": "^4.0",
          "jakub-onderka/php-parallel-lint": "^1.0",
          "sensiolabs/security-checker": "^5.0",
          "friendsofphp/php-cs-fixer": "^2"
    },
```

2.  Create/Update grumphp.yml file.

In the `/doc`-directory, you can find an example `grumphp.yml` file.

#### Configuring grumphp

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

But you can add things separately as well, for example [phpunit](https://phpunit.de/manual/6.5/en/installation.html):

```
$ composer require --dev phpunit/phpunit ^7
```

Then add to steps:

```
- run: ./vendor/bin/phpunit --configuration phpunit.xml tests
```

This works for phpcs and other packages as well. They will appear in `vendor/bin`.

#### Run

Check/test code reun below command before push in git.

```sh
php ./vendor/bin/grumphp run
```
