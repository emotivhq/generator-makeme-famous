## Cordova applications
When scaffolding a mobile app (`yo makeme:target mobile-app --mobile`), this will create a `cordova/mobile-app` folder under `client`.

This folder contains hooks and resources (icons and spashs) that will be copied over during the `dist` gulp task.

### Generate Icons
To generate icons and splashes from a single icon file you can execute
```
gulp cordova:icon
```
It expects an `icon.png` file located in `./client/icons/mobile-app` folder.

The plugins needed for the mobile app must be added in the `./client/cordova/mobile-app/hooks/010_install_plugins.js` file.  The hook is responsible for installing them on relevant platforms.

First - execute `gulp dist --t mobile-app` (with additional `--mode` option i.e `dev` or `prod`), in order to build the `dist` folder.

### Build Mobile platforms
Then - build the mobile platforms.   

**Run:**
```bash
cd dist/mobile-app/<dev or prod>/
cordova platform add <ios or android>
```

When running `gulp browsersync --target mobile-app`  - the task will detect that `mobile-app` is a mobile app, and will automatically launch both a browser-sync browser window and a livereload emulator.   

You can pass an addition `--platform` option to tell it which emulator you want (ios, android, etc...).   

If you don't pass `--platform` it will choose the value from `constants.js` (`constants.cordova.platform`).

### Device Testing
When you are done with testing the app in the browser or the emulator, you can attach your phone device via an USB cable and run: 
```bash
gulp cordova:run
```

If you want to upload your app to **testfairy**, first make sure you fill in the api_key for **testfairy** in `gulp_tasks/common/constants.js`,    
and then simply run
```bash
gulp cordova:testfairy
```

### Cordova Content Security Policy
The `index.html` is configured to be permissive.
Adjust the meta tags `Content-Security-Policy` to our needs. Reference is here : http://content-security-policy.com/ 
