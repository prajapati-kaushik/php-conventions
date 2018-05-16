## Prefered PHP libraries

Here's a list of basic libraries that we enjoy using.

To keep our dependency management simple, and prevent people from learning about multiple libraries that do similar things, we strongly encourage using common libraries that are "commonly used" among other PHP developers

* silex/silex For web services and APIs (request/response handling)
* symfony/http-foundation For request/response classes (PSR-7 considered for future projects)
* PDO For database connectivity
* doctrine/dbal For more advanced use-cases
* monolog/monolog For logging
* herald-project/client-php For transactional messages (email, sms, etc)
* linkorb/stored-client Image handling
* crodas/service-provider For configuring services
* symfony/routing For route definitions (implied through Silex)
* symfony/yaml .yaml file parsing
