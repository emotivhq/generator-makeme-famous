## Browserify/Webpack and Namespaces
At the heart of all of this Universal Javascript `awesome`, we use `browserify`. If you've ever built Node apps (we have), you'll feel at home with `browserify`. Alternatively, you can use `webpack` to bundle together the client javascript files.  
To switch between `browserify` or `webpack` change the constant value `moduleManager` in `gulp_tasks/common/constants.js` (`'browserify'` or `'webpack'`)

### Name Collision
Since Angular modules do not prevent name collision, each scaffolded component gets an unique full name composed like this:

```
[main app name].[module name].[component name]
```
Make oure tp use that full name with dependency injection (DI).

### Requiring modules from other modules  
To require a module from another one, use the following example:

**Example Use Case**

Let's say we have 2 modules, `common` and `analytics`. Since `common` is our base module we first need to connect `analytics` to it with a `require`. 

Do this in the `module.exports` in `index.js` for `common`, right after the `require` for `angular`. (Make sure to pass the namespace argument to the `require`.) 
```js
var angular = require('angular');
var analytics = require('../analytics')(namespace);
```

Now that we have an `analytics` object that has been passed the `namespace`, we can dependency inject the module using `analytics.name`. Just inject the module in an app.
```js
var app = angular.module(fullname, [..., analytics.name]);
```

Finally, the app needs to not only have modules injected but also to  be able to store the names of those modules in an easily accessible location. Attach a `namespace` object to `app` and give it an `analytics` property equal to `analytics.name`.
```js
app.namespace = app.namespace || {};
app.namespace.analytics = analytics.name;
```

We now have a reference between the 2 modules.  Note that the name of the modules are never hard coded :)

We can very easily talk about the `analytics` module from any subcomponent in `app`, but beyond that, we can just as easily get the name of any of component of `analytics`. 

Let's see how. Say that we've created a service on `analytics` called `mixpanelService`. We want to use that service in the `home` controller of the `common`module.

If we scaffolded `mixpanelService` using the generator we won't need to touch anything. If not go into our file and make sure that the name provided to `app.factory` looks like `app.name + '.' + servicename`, which in this case evaluate as 
```js
app.name --> 'main.analytics'
servicename --> 'mixpanel'
```
After being created, the `service.name` will look like `'main.analytics.mixpanel'`

To inject `mixpanelService` into `common`'s `home` controller, go to `/scripts/common/controllers/home.js` and dependency inject the service name appended to the pointer to `analytics.name` that we made before into our `deps` array:

```js
var deps = [app.namespace.analytics + '.mixpanel'];

function controller(mixpanel) {
...
}
```

Again no hard coded namespace, and only one point of attachment between the modules. `badassery`.