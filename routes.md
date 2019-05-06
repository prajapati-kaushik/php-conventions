## Routes

* Store your routes in `/config/routes.yml`
* Never use a closing slash on routes. Good: `/x/y/z` Bad: `/x/y/z/`
* Always use plurals for resource urls Good: `/books/12` Bad: `/book/12`
* The main resource url always provides a listing or search: /books lists all books
* If your route is an "action" on a resource (for example "delete" or "print"), put the action at the end of the route. Good: `/books/12/print` Bad: `/books/delete/12`


### Symfony 4 project routes create with annotation, above each controller action.

```php
        /**
        * @Route("/cards", name="admin_card_index", methods="GET")
        */
        public function indexAction()
        {

        }

```
Controller actions route has comment route url part put on Classname.

```php

    /**
     * @Route("/admin/cards")
     */
    class CardAdminController extends bstractController
    {
        /**
        * @Route("", name="admin_card_index", methods="GET")
        */
        public function indexAction()
        {

        }

        /**
        * @Route("/{id}", name="admin_card_view", methods="GET")
        */
        public function viewAction(Card $card)
        {

        }
    }
```

* route name prefix with parent direcotry name. like  above example: admin_card_index.

* Common routes samples:

    * /books   books index/list page.
    * /books/{id}  book details/view page. book has no view page use route for edit also.
