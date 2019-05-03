Webpack Encore
==============

Symfony use webpack Encore.

Webpack Encore is a simpler way to integrate Webpack into your application. It wraps Webpack, giving you a clean & powerful API for bundling JavaScript modules, pre-processing CSS & JS and compiling and minifying assets. Encore gives you professional asset system that's a delight to use.


Basic overview refere: https://symfony.com/doc/current/frontend.html



* Symfony 4 project setup create files in root path.
https://symfony.com/doc/current/frontend/encore/installation.html

  1.  package.json    ___mention required project list.___
  2. webpack.config.js  ___This is the main config file for both Webpack and Webpack Encore___


* Use node.js for steup. install node and npm in your system.

*  Run console Command for install packages.
```
     path-project-director$ npm install
```

* Modify css and js file under /assets directory.

* Run console command for generate  files.

```
     path-project-director$ node_modules/.bin/encore dev
```

* Incldue js and css file in  teamplate study : https://symfony.com/doc/current/frontend/encore/simple-example.html


```twig
{% block stylesheets %}
    {{ encore_entry_link_tags('app') }}
    {% block stylesheets_custom %}{% endblock %}
{% endblock %}
```

```twig
{% block scripts %}
    {{ encore_entry_script_tags('app') }}
    {% block scripts_custom %} {% endblock %}
{% endblock %}
```

### package.json
package.json sample.

````json
{
    "devDependencies": {
        "@symfony/webpack-encore": "^0.22.0",
        "webpack-notifier": "^1.6.0",
        "bootstrap": "^4.1.1",
        "bootswatch": "^4.1.1",
        "font-awesome": "^4.7.0",
        "node-sass": "^4.11.0",
        "sass-loader": "^7.1.0",
        "popper.js": "^1.14.3",
        "jquery": "^3.3.1",
        "less-loader": "^3.0.0"
    },
    "license": "UNLICENSED",
    "private": true,
    "scripts": {
        "dev-server": "encore dev-server",
        "dev": "encore dev",
        "watch": "encore dev --watch",
        "build": "encore production --progress"
    }
}
````


### webpack.config.js
```javascript
var Encore = require('@symfony/webpack-encore');

Encore
    // directory where compiled assets will be stored
    .setOutputPath('public/build/')
    // public path used by the web server to access the output path
    .setPublicPath('/build')
    // only needed for CDN's or sub-directory deploy
    //.setManifestKeyPrefix('build/')

    /*
     * ENTRY CONFIG
     *
     * Add 1 entry for each "page" of your app
     * (including one that's included on every page - e.g. "app")
     *
     * Each entry will result in one JavaScript file (e.g. app.js)
     * and one CSS file (e.g. app.css) if you JavaScript imports CSS.
     */
    .addEntry('app', './assets/js/app.js')
    .addEntry('signup', './assets/js/frontend.js')

    // When enabled, Webpack "splits" your files into smaller pieces for greater optimization.
    .splitEntryChunks()

    // will require an extra script tag for runtime.js
    // but, you probably want this, unless you're building a single-page app
    .enableSingleRuntimeChunk()

    /*
     * FEATURE CONFIG
     *
     * Enable & configure other features below. For a full
     * list of features, see:
     * https://symfony.com/doc/current/frontend.html#adding-more-features
     */
    .cleanupOutputBeforeBuild()
    .enableBuildNotifications()
    .enableSourceMaps(!Encore.isProduction())
    // enables hashed filenames (e.g. app.abc123.css)
    .enableVersioning(Encore.isProduction())

    // enables @babel/preset-env polyfills
    .configureBabel(() => {}, {
        useBuiltIns: 'usage',
        corejs: 3
    })

    // enables Sass/SCSS support
    .enableSassLoader()

    // uncomment if you use TypeScript
    //.enableTypeScriptLoader()

    // uncomment to get integrity="..." attributes on your script & link tags
    // requires WebpackEncoreBundle 1.4 or higher
    //.enableIntegrityHashes()

    // uncomment if you're having problems with a jQuery plugin
    .autoProvidejQuery()

    // uncomment if you use API Platform Admin (composer req api-admin)
    //.enableReactPreset()
    //.addEntry('admin', './assets/js/admin.js')
;

module.exports = Encore.getWebpackConfig();
```
