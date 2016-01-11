## Gulp tasks
Main mobile tasks:
```
gulp cordova:run    # Run cordova run (accepts a --platform option)
gulp test           # Run lint, unit tests, and e2e tests
gulp browserify     # Generate a distribution folder using browserify
gulp cordova:image  # Generate the cordova icons and splashs
gulp dist           # Distribute the application
```
Main web tasks:
```
gulp browsersync    # Creates a browser-sync server, it will display its url, it watches for js / css / scss / html file changes and inject automatically the change in the browser
gulp test           # Run lint, unit tests, and e2e tests
gulp browserify     # Generate a distribution folder using browserify
gulp dist           # Distribute the application
```


All gulp tasks:

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
