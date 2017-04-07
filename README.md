# api documentation for  [gulp-jslint (v1.0.10)](https://github.com/karimsa/gulp-jslint#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-jslint.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-jslint) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-jslint.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-jslint)
#### The classic and strict javascript lint-tool for gulp.js

[![NPM](https://nodei.co/npm/gulp-jslint.png?downloads=true)](https://www.npmjs.com/package/gulp-jslint)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-jslint/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp-jslint_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-jslint/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-jslint/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-jslint/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Karim Alibhai"
    },
    "bugs": {
        "url": "https://github.com/karimsa/gulp-jslint/issues"
    },
    "dependencies": {
        "chalk": "^1.1.3",
        "gulp-util": "^3.0.7",
        "jshint-stylish": "^2.2.0",
        "jslint": "0.10.3",
        "map-stream": "0.0.6",
        "rc": "^1.1.6",
        "strip-ansi": "^3.0.1"
    },
    "description": "The classic and strict javascript lint-tool for gulp.js",
    "devDependencies": {
        "codeclimate-test-reporter": "0.4.0",
        "gulp": "^3.9.1",
        "istanbul": "^0.4.4",
        "rimraf": "2.5.4",
        "tape": "^4.6.0",
        "vinyl": "^2.0.1"
    },
    "directories": {},
    "dist": {
        "shasum": "4e3a0146b4fc7b43a96e9ecb46d185bd5e59de97",
        "tarball": "https://registry.npmjs.org/gulp-jslint/-/gulp-jslint-1.0.10.tgz"
    },
    "gitHead": "84753f4ba0283ad2bcf79bee6d65286fe60881a6",
    "homepage": "https://github.com/karimsa/gulp-jslint#readme",
    "keywords": [
        "gulp",
        "gulpplugin",
        "jslint",
        "lint",
        "code quality"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "karimsa",
            "email": "k4rim.sa@gmail.com"
        }
    ],
    "name": "gulp-jslint",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/karimsa/gulp-jslint.git"
    },
    "scripts": {
        "codeclimate": "cat coverage/lcov.info | node_modules/.bin/codeclimate-test-reporter",
        "coverage": "istanbul cover test/test-gulp.jslint.js --report lcovonly",
        "pretest": "gulp",
        "rm": "rimraf coverage",
        "test": "npm run coverage && npm run codeclimate && npm run rm"
    },
    "version": "1.0.10"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-jslint](#apidoc.module.gulp-jslint)
1.  [function <span class="apidocSignatureSpan">gulp-jslint.</span>reporter (name, options)](#apidoc.element.gulp-jslint.reporter)



# <a name="apidoc.module.gulp-jslint"></a>[module gulp-jslint](#apidoc.module.gulp-jslint)

#### <a name="apidoc.element.gulp-jslint.reporter"></a>[function <span class="apidocSignatureSpan">gulp-jslint.</span>reporter (name, options)](#apidoc.element.gulp-jslint.reporter)
- description and source-code
```javascript
reporter = function (name, options) {
    options = options !== undefined ? options : {};
    var reporter = name || 'default';

    // if the report is a function, then it does not need any options
    if (typeof reporter !== 'function') {
        // if the given reporter is bundled with gulp-jslint,
        // load it. otherwise, try to 'require' the given reporter.
        var createReporter = supported.hasOwnProperty(name) ? supported[name] : require(name);

        // create a reporter with the given options object
        reporter = createReporter(options);
    }

    // if the reporter is not a stream, wrap it with a map-stream
    if (!(reporter instanceof Stream)) {
        var stream = map(function (source, next) {
            var value = reporter(fixIndex(source.jslint));
            next(source.jslint.success ? null : new gutil.PluginError('gulp-jslint', 'Failed to lint: ' + source.path), value);
        });
        return stream;
    }

    // for stream reporters, just return
    return reporter;
}
```
- example usage
```shell
...
'''javascript
var gulp = require('gulp');
var jslint = require('gulp-jslint');

gulp.task('default', function () {
    return gulp.src(['source.js'])
            .pipe(jslint({ /* this object represents the JSLint directives being passed down */ }))
            .pipe(jslint.reporter( 'my-reporter' ));
});
'''

If you would like to specify a custom jslint edition to use, set the property 'edition' in your directives object.
These versions should follow what the package node-jslint expects or this property can be set to a pre-loaded jslint
function.
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
