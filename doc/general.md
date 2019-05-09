## General

* Always include a README.md in the root of your project (see details below)
* Always include a .gitignore file
* Always include a LICENSE.md file in the root of your project for public repositories (see details below)

### README.md

Always provide a README.md in the root of your project

### Include detailed instructions:
    
* How to downloading the code (`git clone` command)
* How to download/install any dependencies (Composer, NPM, Bower, etc.)
* How to initialize database schema (if applicable)
* How to copying any `.dist` files to real files
* How to configure parameter files, environment variables, etc.
* How to start a server for development (using integrated PHP web-server)

### Other requirements:

* Include the "Brought to you by the LinkORB Engineering team" banner at the end of the file (You can use <a href="https://github.com/linkorb/template-php/blob/master/README.md">this template</a>)
* Include licensing information

### LICENSE file

Usually all projects start as private repositories. A private repository does not need a `LICENSE` file, it is always considered proprietary.

If you work on a public repository, by convention it will follow the MIT license, and it should include a copy of this file in your repository: https://github.com/linkorb/template-php/blob/master/LICENSE

## Test coverage
* Any new code SHOULD be covered by unit tests. Ideally also should be covered changed code without tests.
* Any PR SHOULD NOT have failed tests
