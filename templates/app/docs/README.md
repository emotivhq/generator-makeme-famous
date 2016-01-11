# `Makeme Famous` - A Universal Javascript generator for #coolkids 
`Makeme Famous` is a universal javascript stack generator for Yeoman - featuring Angular, Browserify, Material, Semantic, Ionic and Famous. 

[ ![Codeship Status for giftstarter/generator-makeme-famous](https://codeship.com/projects/24ba9cc0-9793-0133-aba0-668c447e66c0/status?branch=master)](https://codeship.com/projects/125853)

> Are you looking for [**`Makeme`**](https://www.github.com/giftstarter/generator-makeme) Fullstack? 


## GyShiDo with `makeme-famous`
To get shit done, here's a quick list of useful info. 

1. [Universal Javascript](#Welcome-to-Universal-Javascript) with Angular
2. [Setting Up](#setting-up)
3. [Typical workflows](#typical-workflows)
4. Overview of [client folder](#the-client-folder)
5. Overview of [module folder](#the-module-folder)
6. [Gulp tasks](#gulp-tasks)
7. [Adding Bower packages](#adding-bower-packages)
8. → [Generator](./generators.md) docs 
9. → [Ionic](./ionic.md) docs
10. → [Browserify](./browserify.md) docs
11. [Changelog](#changelog)
12. [Upgrade](#upgrade)

<img src="http://yeoman.io/static/illustration-home-inverted.1f863f34ba.png" width="500px">

---

<img src="http://www.w3schools.com/angular/pic_angular.jpg" width="50px"><img src="http://ionicframework.com/img/ionic-logo-blog.png" width="50px"><img src="http://www.codingpedia.org/wp-content/uploads/2014/04/gulp-2x.png" width="50px"><img src="https://avatars.githubusercontent.com/mcfly-io?s=128" width="50px"><img src="http://www.semantic-ui.cn/images/logo.png" width="50px"><img src="https://wordimpress.com/assets/icon-grunt.png" width="50px"><img src="http://yeoman.io/static/yeoman-02.dc21b7fc1d.png" width="50px"><img src="http://images.frandroid.com/wp-content/uploads/2012/05/cordova_bot.png" width="50px">

---

## Welcome to Universal Javascript
![](https://cdn-images-1.medium.com/max/1600/1*pkA5znpcqqmIwZRXesioGA.png)
Javascript that can run both in the client (browser) and server (ie - [Node.js](https://nodejs.org/)) is here...[read more about it here](https://medium.com/@mjackson/universal-javascript-4761051b7ae9).

### Stack Generator
This `yeoman` universal javascript application stack generator features [Angular](https://angular.io/), [Ionic Framework](http://ionic.io/), [Semantic UI](http://semantic-ui.com/), [Angular Material](https://material.angularjs.org/latest/) (or Angular Bootstrap), [Angular Famous](http://famo.us/angular), and more.

Here are some of the main capabilities:

* Angular best practices ([`feature folder`](http://www.johnpapa.net/angular-growth-structure/) structure)
* SASS AND LESS enabled
* [`jshint`](http://jshint.com/), [`jscsc`](http://jscs.info/), [`eslint`](http://eslint.org/) enabled for better quality code
* [Browserify](http://browserify.org/) or [Webpack](https://webpack.github.io/) (you can switch them out)
* [Karma](https://karma-runner.github.io/) configured with [Code Coverage](https://karma-runner.github.io/0.8/config/coverage.html)
* [Protractor](http://www.protractortest.org/) E2E Angular testing
* [Browser-sync](https://www.browsersync.io/) for synchronised browser testing
* Continuous integration with [Travic CI](https://travis-ci.org/)
* [TestFairy](http://testfairy.com/) publishing for mobile testing
* [Ionic.io](https://apps.ionic.io) publishing
* [ES6](http://www.es6js.com/)/[7](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_7_support_in_Mozilla) supported by using [`the babel`](https://babeljs.io/)

---

> **NOTE:**   
> This uses [generator-sublime](https://www.npmjs.org/package/generator-sublime) to scaffold common dot files (`.jshintrc`, `.eslintrc`, etc...).   

## Setting up
In order to get the best experience, you have to install a couple of global npm packages, like Gulp, Yemoan, and more. Feel free to tweak `./bin/prepublish.sh` to add additional requirements.

###Prerequisites
#### Auto install
Execute the following command:

```bash
$ ./bin/prepublish.sh
```

This will install, among others, the following packages globally:

* gulp
* browserify
* watchify
* webpack
* cordova
* ionic (cli) (Cordova wrapper)


### Install the generator
Install dependencies and `generator-makeme-famous`:
```bash
 npm install -g yo gulp bower mocha istanbul codeclimate-test-reporter generator-makeme-famous
```



#### A few things to note:

1. If you have issues (like `$ yo: command not found`) - first run `npm install -g yo` & `npm install --global gulp`
2. If you have existing project modify the name of the generator in your `.yo-rc.json` file 
3. If you need to update Node, do this:
  1. `npm cache clean -f`
  2. Install [nvm](https://github.com/creationix/nvm#install-script)
  3. `nvm install 5.3.0`
  4. `nvm use 5.3.0`.

---

## Typical workflows
Some tyical workflows to get started with.

### New app
```
$ yo makeme-famous:target newapp
```
Or
```
yo makeme-famous:target newapp --mobile
```

### New module
A typical new module workflow would look like this:
```bash
$ mkdir new-app && cd $_
$ yo makeme-famous:module common
$ yo makeme-famous:controller common hello

> Add some content to client/index.html : <h2 ng-controller="new-app.common.hello as helloCtrl">{{helloCtrl.message}}</h2>

$ gulp browsersync
$ gulp watch
```

### New controller, existing module
A typical new controller workflow would look like this:
```bash
$ cd new-app
$ yo makeme-famous:controller common hello

> Add some content to client/index.html : <h2 ng-controller="new-app.common.hello as helloCtrl">{{helloCtrl.message}}</h2>

$ gulp browsersync
$ gulp watch
```

> **TIP:** `gulp browsersync` accepts an option `--no-browser` if you do not want to automatically open a browser

---

 **NOTE:** `gulp browsersync` accepts an option `--https` if you want to force an HTTPS connection you can also control http vs https using in `gulp_taks/common/constants.js` -> `serve.https` boolean

#### - To see more, check out the [Generator docs](./docs/generators.md).


## The Client folder
When building a new app, the generator will ask you to provide the name of the folder containing the client source code, and it will save this value in `.yo-rc.json` file (`clientFolder` entry).   If you rename the `client` folder, make sure you also modify the value stored in `.yo-rc.json`

## Gulp tasks
Here is a set of simple gulp tasks available:
```
gulp help           # List the main gulp tasks
gulp lint           # Run lint
gulp test           # Run lint, unit tests, and e2e tests
gulp unit           # Run lint and unit tests (karma for client + mocha for server)
gulp karma          # Run karma client unit tests
gulp mocha          # Run mocha server unit tests
gulp e2e            # Run protractor for end to end tests
gulp browserify     # Generate a distribution folder using browserify
gulp webpack:run    # Generate a distribution folder using webpack
gulp style          # Generate a main.css file
gulp browsersync    # Creates a browser-sync server, it will display its url, it watches for js / css / scss / html file changes and inject automatically the change in the browser
gulp dist           # Distribute the application
gulp cordova:image  # Generate the cordova icons and splashs
gulp cordova:run    # Run cordova run (accepts a --platform option)
```

> See the [full gulp docs](./docs/gulp.md) for all of the yummy Gulp tasks. 


The gulp tasks share a constant file located at `gulp/common/constants.js`. Feel free to modify it.   
The constants are resolved against the `--target` option. The default value for `--target` is `app`.

> To better understand the gulp task system have a look at the docs of [gulp-mux](https://github.com/mcfly-io/gulp-mux) 



## Adding Bower packages
You should always prefer an `npm` package instead of a `bower` package. Most of client side libraries nowadays exist as both npm and bower packages. But sometimes it is not the case and you have to deal with a bower package. Here's how to do it elegantly.

To include a third party `bower` package do the following:

* `bower install --save thepackage`
* modify `package.json` `browser` section to include a path to the global minified javascript file of the package
* adjust the **font** gulp constants (`gulp/common/constants.js`) to include the relevant fonts of the package (if applicable)
* if the package exposes a global `.scss` file import it into `client/styles/main.scss` and ajdust eventually the variable for the path font (should be `../fonts`)
* if the package only exposes a `.css` file adjust the **css** file constants (`gulp/common/constants.js`) to include it
* if the package relies on other libraries
  * Either add a browser-shim section (but this will only work with `browserify`, not `webpack`)
  * Or make sure to require the dependencies in the code just before you `require` the package.



## Changelog

Recent changes can be viewed on Github on the [Releases Page](https://github.com/giftstarter/makeme-famous/releases)


## Upgrade
Here is the core generator upgrade process.

**1:**
```bash
npm update -g generator-makeme-famous
```
**2:**
```bash
git pull github master
```


