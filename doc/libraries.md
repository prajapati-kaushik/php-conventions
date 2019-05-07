## Preferred PHP libraries

Here's a list of basic libraries that we enjoy using.

To keep our dependency management simple, and prevent people from learning about multiple libraries that do similar things, we strongly encourage using common libraries that are "commonly used" among other PHP developers

* `silex/silex`: Web services and APIs (request/response handling)
* `symfony/http-foundation`: Request/response classes (PSR-7 considered for future projects)
* `PDO`: Database connectivity
* `doctrine/dbal`: More advanced use-cases
* `monolog/monolog`: Logging
* `herald-project/client-php`: Transactional messages (email, SMS, etc)
* `linkorb/stored-client`: Image handling
* `crodas/service-provider`: Configuring services
* `symfony/routing`: Route definitions (implied through Silex)
* `symfony/yaml`: .yaml file parsing
