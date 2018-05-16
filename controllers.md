## Controllers

* Never use `exit`, `var_dump`, `echo`, `die` in controllers. Always return a `Response` object.
* Keep controller code small. Any functionality should be implemented in Repositories, Models or other classes.
* Don't put too many controller functions in 1 class. Split them by resource if the class becomes too big.
