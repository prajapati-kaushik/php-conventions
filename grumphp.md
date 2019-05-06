## GrumPHP

We're using [GrumPHP](https://github.com/phpro/grumphp) to automatically check for code-quality.

#### GrumPHP  Symfony 4 Install and use

1. Installl packages under require-dev section in you composer.json file. With GrupmPHP checking thats.

```json
    "require-dev": {
          "phpro/grumphp": "^0.14",
          "sebastian/phpcpd": "^4.0",
          "jakub-onderka/php-parallel-lint": "^1.0",
          "sensiolabs/security-checker": "^5.0",
          "friendsofphp/php-cs-fixer": "^2"
    },
```

2.  Create/Updte grumphp.yml file, after install package generate in project root.
3.  /doc directory you can find gurmphp.yaml.

#### Run

Check/test code reun below command before push in git.

```sh
php ./vendor/bin/grumphp run

```
