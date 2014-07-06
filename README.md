# resolve-dep [![NPM version](https://badge.fury.io/js/resolve-dep.png)](http://badge.fury.io/js/resolve-dep)

> Return an array of resolved filepaths for require-able local or named npm modules. Wildcard (glob) patterns may be used.

Similar in concept to [matchdep](https://github.com/tkellen/node-matchdep) and [load-grunt-tasks](https://github.com/sindresorhus/load-grunt-tasks), but returns an array of fully resolved file paths to _any local modules or npm modules listed in package.json dependencies_.

## Install
Install with [npm](npmjs.org):

```bash
npm i resolve-dep --save-dev
```

## Usage

```js
var resolve = require('resolve-dep');
resolve( patterns, options )
```

## API

### .resolveDep()

Resolve both npm packages and local modules by:

  1. Attempting to expand glob patterns to local modules, then
  1. Attempting to match glob patterns to deps in package.json

**Examples:**

```js
// file path
resolve('foo/bar.js');
// glob patterns
resolve('foo/*.js');
// named npm module (installed in node_modules)
resolve('chai');
// combination
resolve(['chai', 'foo/*.js']);
```

* `patterns` {Array|String}: Glob patterns for files or npm modules. 
* `options` {Object}  
* `return` {Array} 


### .resolveDep.npm()

Resolve npm packages in node_modules by matching glob patterns to deps in
package.json. NPM modules will only be resolved if they are defined in
one of the "dependencies" fields in package.json.

```js
// resolve npm modules only
resolve.npm(['chai', 'lodash']);
```

* `patterns` {Array|String} 
* `options` {Object}  
* `return` {Array} 


### .resolveDep.local()

Resolve local modules by expanding glob patterns to file paths.

```js
// resolve local modules only
resolve.local(['a/*.js', 'b/*.json']);
```

* `patterns` {Array|String} 
* `options` {Object}  
* `return` {Array}


### Options

Type: `object`

The options object supports any [globby](https://github.com/sindresorhus/globby) options, as well as the following:


### patterns

Type: `string|array`

The file path, glob pattern, or name of the npm module to resolve.

**File paths**

```js
resolve('templates/*.hbs')
resolve(['a/*.hbs', 'b/*.hbs'])
```

**NPM modules**

```js
resolve('*')
resolve(['grunt-*', 'gulp-*'])
resolve(['grunt-*', 'gulp-*'], {type: 'devDependencies'})
resolve(['lodash', 'assemble']);
```

#### options.config
Type: `Object`
Default value: `package.json`

Pass an explicit config object to use instead of package.json.

#### options.type

Type: `String|Array`

Default value: `all`

Valid values: `all|dependencies|devDepencies|peerDependencies`

Any valid npm dependency field that can be used in package.json is a valid value for this option.

**Examples:**

```js
// resolve chai and mocha, if in devDependencies, otherwise an empty array
resolve(['chai', 'mocha'], {type: 'devDependencies'});
// resolve lodash if in dependencies, otherwise an empty array
resolve(['lodash'], {type: 'dependencies'});
// all dependencies
resolve(['*'], {type: 'dependencies'});
// all dependencies, devDependencies and peerDependencies
resolve('*');
```


## Author

**Jon Schlinkert**
 
+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert) 

## License
Copyright (c) 2014 Jon Schlinkert, contributors.  
Released under the MIT license

***

_This file was generated by [verb-cli](https://github.com/assemble/verb-cli) on July 06, 2014._
