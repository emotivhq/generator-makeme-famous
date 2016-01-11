## Ionic.io platform

![](http://ionic.io/img/iologo.png)

The gulp system also includes some basic tasks for ensuring that the ionic projects in `dist/` are able to make use of the [apps.ionic.io](https://apps.ionic.io/) platform. These are found in `gulp_tasks/tasks/ionic.js`. 

> To use the ionic.io platform services, scaffold a mobile target (with `yo makeme-famous --mobile` or `yo makeme-famous:target --mobile`) and then create a project on [apps.ionic.io](https://apps.ionic.io/). 

### Publishing Setup
Make sure that the target has the correct properties from the correct ionic project; most importantly the `app_id`, `api_key`, and `name` from [apps.ionic.io](http://docs.ionic.io/docs/io-api-keys). 

Fill these in inside the `gulp_tasks/common/constants.js` file, in the `ionic` section for your target. If planning to use `Ionic Push`, make sure to also include the `dev_push: true` property, so the app will know to register for the correct push notifications. 

>If is not an entry in `constants.ionic` for the target, simply copy and fill in the one for the `app` target. Make sure to end up with a `constants.ionic` that looks like this:
    ```js
        ionic: {
            ionicPlatform: { ... },
            app: { ... },
            <yourtargetname>: {  // fill this object with the *correct* [ionic.io](http://ionic.io/) details
                app_id: '123abcd',
                api_key: '0123456789abcdefghij0123456789abcdefghij012345',
                name: 'GS Main Ionic App',
                dev_push: true
            }
        }
    ```

After saving the constants, run

```sh
gulp ionic:platformcopy --target=<targetname>
```

to copy over the [`ionic-platform-web-client`](https://github.com/driftyco/ionic-platform-web-client) bundle into the client folder, injecting the project's `ionic.io` data into it along the way.

Next, uncomment the line that says `require('./ionic.io.bundle.min-<yourtargetname>');` at [`client/scripts/main<targetsuffix>.js:14`](https://github.com/giftstarter/generator-makeme-famous/blob/master/templates/target/scripts/main.js#L14) as well as the module dependency for `'ionic.service.core'` that follows it. Finally comment out the script include of `cordova.js` in [`client/index<targetsuffix>.html:22`](https://github.com/giftstarter/generator-makeme-famous/blob/master/templates/target/index.html#L22), since the `ionic.io.bundle.min.js` will automatically load the correct instance of the `cordova.js` script.

Currently `'ionic:deploy'` is the only entry-point task, and it runs a `'dist'` and then handles the uploading and optional deployment of a project update to the ionic deploy server. We need to specify a target with a `--target=<targetname>` and then which mode we're using (usually `prod`) with `--mode=<dev|prod>`. After that, add the `--note` and `--deploy` flags as specified by the [`ionic deploy` cli](http://docs.ionic.io/docs/deploy-deploying-updates).

More tasks to integrate with other ionic.io services are coming soon, but in the meantime, if you write your own, feel free to make a PR to [`generator-sublime`](https://github.com/mcfly-io/generator-sublime). The file to edit is [`templates/gulps/tasks/ionic.js`](https://github.com/mcfly-io/generator-sublime/tree/master/templates/gulps/tasks/ionic.js). 

> Refer to the [apps.ionic.io docs](http://docs.ionic.io/) for inspiration, and then look at [`ionic-app-lib`](https://github.com/driftyco/ionic-app-lib) (the library that powers [`ionic-cli`](https://github.com/driftyco/ionic-cli)) to see how you can hook into the ionic system under the hood.