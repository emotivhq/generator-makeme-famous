## Testing

### Unit + E2E
To run unit test and e2e tests for the `yeoman` project use the following command:
```
gulp test
```
### Karma - no linting
To just run karma and are not interested yet in linting files - run:
```
gulp karma
```
### Debug
To debug the code use the --debug flag
```
gulp karma --debug
```
### Karma in the background
You can eventually also run karma in the background, with auto refresh using the option `--start`
```
gulp karma --start
```

###Karma module manager
To run karma with a specific bundle manager and a specific module, run:
```
gulp karma --bundler webpack --module common
```
###Mocha
To just run mocha and are not interested yet in linting files - run:
```
gulp mocha
```

###Unit

Just run a specific unit test:
```
mocha test/app.test.js -r test/helpers/globals.js
```
This will tell mocha to run only the tests located in `test/app.test.js` (The -r option is necessary here to add global configuration file for mocha, when using gulp the `globals.js` is added automatically)

### E2E
Run e2e tests using the following command:
```
gulp e2e # the same as gulp e2e --coverage --target=app
```
This will `dist` and instrument the source code so you get code coverage, and uses the default target.

### E2E - Bypass `dist`
If you didn't change the source code you can bypass the dist:
```
gulp e2e --skip-dist
```
### Target testing
If you want another target:
```
gulp e2e --target=dashboard
```