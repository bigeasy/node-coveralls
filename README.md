#node-coveralls
[![Build Status](https://travis-ci.org/cainus/node-coveralls.png?branch=master)](https://travis-ci.org/cainus/node-coveralls)

[Coveralls.io](https://coveralls.io/) support for node.js.  Get the great coverage reporting of coveralls.io and add a cool coverage button ( like this: ![](https://s3.amazonaws.com/assets.coveralls.io/badges/coveralls_94.png) ) to your README.

Installation: Add the latest version of `coveralls` to your package.json.

This script ( `bin/coveralls.js` ) can take standard input from any tool that emits the lcov data format (including [mocha](http://visionmedia.github.com/mocha/)'s [LCov reporter](https://npmjs.org/package/mocha-lcov-reporter)) and send it to coveralls.io to report your code coverage there.  It needs to run from [travis-ci](http://about.travis-ci.org/docs/user/languages/javascript-with-nodejs/) to work.

Instrumenting your app for coverage is probably harder than it needs to be (read [here](http://www.seejohncode.com/2012/03/13/setting-up-mocha-jscoverage/) or [here](http://tjholowaychuk.com/post/18175682663/mocha-test-coverage)), but that's also a necessary step. 

Once your app is instrumented for coverage, and building in travis-ci, you just need to pipe the lcov output to `./node_modules/coveralls/bin/coveralls.js`.

In mocha, if you've got your code instrumented for coverage, the command for a travis build would look something like this:
```console
YOURPACKAGE_COVERAGE=1 ./node_modules/.bin/mocha test -R mocha-lcov-reporter | ./node_modules/coveralls/bin/coveralls.js
```
Note: this will only run on travis-ci, where a necessary TRAVIS_JOB_ID environment variable will exist.

Check out an example [Makefile](https://github.com/cainus/urlgrey/blob/master/Makefile) from one of my projects for an example, especially the test-coveralls build target.  Note: Travis runs `npm test`, so whatever target you create in your Makefile must be the target that `npm test` runs (This is set in package.json's 'scripts' property).

