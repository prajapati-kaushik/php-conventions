## composer.json


* Provide a clear `description`
* Include the keyword "linkorb" (lowercase, one word) in the keywords list, among other relevant keywords.
* Include the license in the `composer.json` file
* Include engineering@linkorb.com as one of the authors. Include your own name too if you prefer (optional).
* Include licensing information. For example
The `composer.json` file should also refer to the MIT license using this snippet:

```
"license": "MIT"
```
* development/testing/debug related packages add under `require-dev` section.


### Provide details in composer.json file
    modify details as per you project. Like Name, description and homepage link.

```json
    "name": "linkorb/xxx",
    "description": "Symfony 4 project: It lists postalcodes of areas which require more care from healthcare providers",
    "homepage": "https://github.com/linkorb/xxx",
    "keywords": ["form", "linkorb"],
    "type": "application",
    "license": "proprietary",
    "authors": [
        {
          "name": "LinkORB Engineering",
          "email": "engineering@linkorb.com",
          "role": "Development"
        }
      ],
```
