## Controllers

* Never use `exit`, `var_dump`, `echo`, `die` in controllers. Always return a `Response` object.
* Keep controller code small. Any functionality should be implemented in Repositories, Models or other classes.
* Don't put too many controller functions in 1 class. Split them by resource if the class becomes too big.
* Controllers SHOULD NOT have any either protected/private methods or public methods that are not actions

**These Symfony coding standards are based on the PSR-1, PSR-2 and PSR-4 standards, so you may already know most of them.**

Study more detail: https://symfony.com/doc/current/contributing/code/standards.html#naming-conventions

### Controller and action name.

* Class names MUST be declared in StudlyCaps. E.g. `CardEntity`
* Class names for controllers MUST suffix with `Controller`. Same goes for services, entities and repositories. E.g. `CardEntityController`
* Class constants MUST be declared in uppercase snake case. E.g. `UPPERCASE_SNAKE_CASE`
* Method names MUST be declared in camelCase.
* Controller class names and file name MUST always correspond.
* Each class public Action must suffix with Action. E.g. `indexAction()`
* Try to implement Type Hinting for methods.
* Instead of putting too many controller functions in one class, split them into modules, entities, etc.
* When using repositories, create a separate function to find an entity by a field name and value, for example:
   ```php

        $userRepository->findByUsername($username);

        // src/Repository/UserRepository
        public function findByUsername($username)
        {
            return $this->findBy(['username' => $username]);
        }
    ```
* If possible, try to put logic in a service class. Create service classes under the `src/Service` directory.
