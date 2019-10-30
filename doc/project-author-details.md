# Project Author name and details

* Instead of defining @author details on each file. Provide details in `composer.json` file.
* Since multiple people work on the same projects, it's annoying to update/enhance.

Example:
```php
/**
 * @author fullname <bob@email.com>
 */
```
Composer.json file
```json
    "authors": [
        {
           "name": "LinkORB Engineering",
           "email": "engineering@linkorb.com",
           "role": "Development",
            "homepage": "https://www.linkorb.com/",

        },
        {
            "name": "kaushik prajapati",
            "email": "prajapatikaushik@gmail.com",
            "homepage": "https://github.com/kaushikindianic",
            "role": "Developer"
        }
    ],
```

