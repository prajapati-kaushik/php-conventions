## Routes

* Store your routes in `/config/routes.yml`
* Never use a closing slash on routes. Good: `/x/y/z` Bad: `/x/y/z/`
* Always use plurals for resource urls Good: `/books/12` Bad: `/book/12`
* The main resource url always provides a listing or search: /books lists all books
* If your route is an "action" on a resource (for example "delete" or "print"), put the action at the end of the route. Good: `/books/12/print` Bad: `/books/delete/12`
