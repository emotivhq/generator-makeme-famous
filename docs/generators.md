## Generators

Here is a running list of the currently available generators:

* [makeme](#app)
* [makeme:target](#target)
* [makeme:module](#module)
* [makeme:controller](#controller)
* [makeme:directive](#directive)
* [makeme:filter](#filter)
* [makeme:service](#service)
* [makeme:value](#value)
* [makeme:constant](#constant)
* [makeme:require](#require)


> **Note: Generators are *only* to be run from the root directory of an app.**

### App
Sets up a new AngularJS app, generating all the boilerplate needed to get started. The app generator also installs additional AngularJS modules, such as:

 - angular-mocks
 - angular-animate
 - angular-sanitize
 - angular-ui-router

The main application is called `main`.

**Example:**
```
yo makeme
```

You can choose to scaffold a mobile (cordova) app using the option `--mobile`

**Example:**
```
yo makeme --mobile
```
This will scaffold a config.xml file (suffixed with the app name), and hooks expected by cordova.    In addition the `dist` folder will conform to cordova expectation (`www` sub folder).

### Target
Generate a new target application.  This is useful to share code between several applications (mobile, web, etc...).

Example:
```
yo makeme:target web
```

Produces: 

 - [client/index-web.html](#) 
 - [client/scripts/main-web.js](#)
 - [client/styles/main-web.scss](#)

> **NOTE:**    
> By default the app generates a default application with no suffix. This is equivalent to running the `target` generator with argument `app`

You can choose to scaffold a mobile (cordova) app using the option `--mobile`

**Example:**
```
yo makeme:target mobileapp --mobile
```
This will scaffold a config.xml file (suffixed with the app name), and hooks expected by cordova.  In addition the `dist` folder will conform to cordova expectation (`www` sub folder).


### Module
Generates a new module. All features should be built as a module.

**Example:**
```
yo makeme:module modulename
```

If you don't mention a modulename, `yeoman` will ask you to provide one.

**Produces:** 

 - [client/scripts/modulename/index.js](#) 
 - [client/scripts/modulename/view/home.html](#)


If you do not want any route for the module, you can use the option `--skip-route`   

**Example:**
```
yo makeme:module modulename --skip-route
```

In this case this will only produce: 

 - [client/scripts/modulename/index.js](#)

### Controller
Generates a new controller.

**Example:**
```
yo makeme:controller modulename controllername
```

You need at least a module in order to scaffold a controller.   

If you don't specify arguments, `yeoman` will display the list of existing modules and let you choose one.   

**Produces:** 

- [client/scripts/modulename/controllers/controllername.js](#)
- [client/scripts/modulename/controllers/controllername.test.js](#)
- [client/scripts/modulename/controllers/index.js](#)


### Filter
Generates a new filter.

**Example:**
```
yo makeme:controller modulename filtername
```

You need at least a module in order to scaffold a filter.   
If you don't specify arguments, `yeoman` will display the list of existing modules and let you choose one.   

**Produces:** 

- [client/scripts/modulename/fiters/filtername.js](#)
- [client/scripts/modulename/fiters/filtername.test.js](#)
- [client/scripts/modulename/filters/index.js](#)


### Value
Generates a new value.

**Example:**
```
yo makeme:value modulename valuename
```

You need at least a module in order to scaffold a value.  If you don't specify arguments, `yeoman` will display the list of existing modules and let you choose one.   

**Produces:** 

* [client/scripts/modulename/values/valuename.js](#)
* [client/scripts/modulename/values/valuename.test.js](#)
* [client/scripts/modulename/values/index.js](#)


### Constant
Generates a new constant.

**Example:**
```
yo makeme:value modulename constantname
```

You need at least a module in order to scaffold a constant.   
If you don't specify arguments, `yeoman` will display the list of existing modules and let you choose one.   

Produces: 

* [client/scripts/modulename/constants/constantname.js](#)
* [client/scripts/modulename/constants/constantname.test.js](#)
* [client/scripts/modulename/constants/index.js](#)

### Service
Generates a new service. Use the `--servicetype` option to specify if you want a `service`, a `factory`, or a `provider`.
Default `servicetype` is **`factory`**.

**Example:**
```
yo makeme:service modulename servicename
```
Or
```
yo makeme:service modulename servicename --servicetype=service
```
Or
```
yo makeme:service modulename servicename --servicetype=provider
```

You need at least a module in order to scaffold a service.  If you don't specify arguments, yeoman will display the list of existing modules and let you choose one.   

**Produces:** 

* [client/scripts/modulename/services/servicename.js](#)
* [client/scripts/modulename/services/servicename.test.js](#)
* [client/scripts/modulename/services/index.js](#)

### Directive
Generates a new directive.

Use the `--compile` option to specify if you want `compile`, `pre` and `post` link function (`true`), or just a simple link function (`false`).

> Default `compile` is true.

Example:
```
yo makeme:directive modulename myDirective
```
Or
```
yo makeme:directive modulename myDirective --compile=false
```

You need at least a module in order to scaffold a directive.  If you don't specify arguments, yeoman will display the list of existing modules and let you choose one.   

**Produces:** 

* [client/scripts/modulename/directives/myDirective.html](#)
* [client/scripts/modulename/directives/myDirective.js](#)
* [client/scripts/modulename/directives/myDirective.test.js](#)
* [client/scripts/modulename/directives/index.js](#)


### Require
This generator will not scaffold any files.  Instead it inspects the existing `client` folder and will refresh the needed injected require statements in every file where it is relevant.   

**Example:**
```
yo makeme:require
```