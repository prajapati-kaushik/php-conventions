## Controllers

* Never use `exit`, `var_dump`, `echo`, `die` in controllers. Always return a `Response` object.
* Keep controller code small. Any functionality should be implemented in Repositories, Models or other classes.
* Don't put too many controller functions in 1 class. Split them by resource if the class becomes too big.


**These Symfony coding standards are based on the PSR-1, PSR-2 and PSR-4 standards, so you may already know most of them.**

Study more detail: https://symfony.com/doc/current/contributing/code/standards.html#naming-conventions


### Controller and action name.

* Class names MUST be declared in StudlyCaps.  `CardEntity`
* Class constants MUST be declared in all upper case with underscore separators.
* Method names MUST be declared in camelCase.
* Class Must suffix with  Controller.     `CardEntityController`
* controller class and file name always same.
* If seperate controller file in directoires and directory suffix with controller name.
    Under Src/Controller/Admin directory created classname look like:  ``` CardAdminController ```  filename: ``` CardAdminController.php ```

* Each class public Action must suffix with Action Like:  indexAction()
* Symfony 4 instead of create new object try to inject type hinting.
* Instead of put too many controller functions in one class. Split them into module/entity/decompose/bundle.

* Symfony instead of use repository inbuild function, crate meaning full function and call it
   Exampe:
   ```php
        // Src/Controller/UserController

        $userRepository->findBy(['username' => $username ]);

        // instead of create function in Repositry file and call in coroller like.

        $userRepository->findByUsername($username);

        // Src/Repository/UserRepostirory
            public function findByUsername($username)
            {
                return $this->findBy(['username' => $username]);
            }
    ```
* If possible try to put logic in service class file. Create service files under Src/Service directory. class name suffix with Service.

* Generally class file suffix with there directory name.

    - controller file Src/Controller/UserController
    - Service file  Src/Service/EventService
    - Entity file   Src/Entity/UserEntity
    - Repository file Src/Repository/UserRepositroy.


