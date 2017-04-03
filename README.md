# api documentation for  [routes (v2.1.0)](https://github.com/aaronblohowiak/routes.js)  [![npm package](https://img.shields.io/npm/v/npmdoc-routes.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-routes) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-routes.svg)](https://travis-ci.org/npmdoc/node-npmdoc-routes)
#### Minimalist route matching for javascript

[![NPM](https://nodei.co/npm/routes.png?downloads=true)](https://www.npmjs.com/package/routes)

[![apidoc](https://npmdoc.github.io/node-npmdoc-routes/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-routes_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-routes/build..beta..travis-ci.org/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-routes/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-routes/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Aaron Blohowiak",
        "email": "aaron.blohowiak@gmail.com",
        "url": "http://github.com/aaronblohowiak"
    },
    "bugs": {
        "url": "https://github.com/aaronblohowiak/routes.js/issues"
    },
    "dependencies": {},
    "description": "Minimalist route matching for javascript",
    "devDependencies": {
        "browserify": "^3.30.4"
    },
    "directories": {
        "lib": "."
    },
    "dist": {
        "shasum": "475571192a48f99b6c065dd926bb75e8ae83e8a2",
        "tarball": "https://registry.npmjs.org/routes/-/routes-2.1.0.tgz"
    },
    "engines": {
        "node": "*"
    },
    "gitHead": "f85efed8b5a626130a4a549fdf262f8e885ebb6d",
    "homepage": "https://github.com/aaronblohowiak/routes.js",
    "main": "dist/routes",
    "maintainers": [
        {
            "name": "aaronblohowiak",
            "email": "aaron.blohowiak@gmail.com"
        },
        {
            "name": "raynos",
            "email": "raynos2@gmail.com"
        }
    ],
    "name": "routes",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/aaronblohowiak/routes.js.git"
    },
    "scripts": {
        "prepublish": "mkdir -p dist/ && browserify --require ./index --standalone routes > dist/routes.js",
        "test": "make test"
    },
    "version": "2.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module routes](#apidoc.module.routes)
1.  [function <span class="apidocSignatureSpan">routes.</span>Route (path)](#apidoc.element.routes.Route)
1.  [function <span class="apidocSignatureSpan">routes.</span>Router ()](#apidoc.element.routes.Router)
1.  [function <span class="apidocSignatureSpan">routes.</span>match (routes, uri, startAt)](#apidoc.element.routes.match)
1.  [function <span class="apidocSignatureSpan">routes.</span>pathToRegExp (path, keys)](#apidoc.element.routes.pathToRegExp)



# <a name="apidoc.module.routes"></a>[module routes](#apidoc.module.routes)

#### <a name="apidoc.element.routes.Route"></a>[function <span class="apidocSignatureSpan">routes.</span>Route (path)](#apidoc.element.routes.Route)
- description and source-code
```javascript
Route = function (path){
  //using 'new' is optional

  var src, re, keys = [];

  if(path instanceof RegExp){
    re = path;
    src = path.toString();
  }else{
    re = pathToRegExp(path, keys);
    src = path;
  }

  return {
  	 re: re,
  	 src: path.toString(),
  	 keys: keys
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.routes.Router"></a>[function <span class="apidocSignatureSpan">routes.</span>Router ()](#apidoc.element.routes.Router)
- description and source-code
```javascript
Router = function (){
  //using 'new' is optional
  return {
    routes: [],
    routeMap : {},
    addRoute: function(path, fn){
      if (!path) throw new Error(' route requires a path');
      if (!fn) throw new Error(' route ' + path.toString() + ' requires a callback');

      if (this.routeMap[path]) {
        throw new Error('path is already defined: ' + path);
      }

      var route = Route(path);
      route.fn = fn;

      this.routes.push(route);
      this.routeMap[path] = fn;
    },

    removeRoute: function(path) {
      if (!path) throw new Error(' route requires a path');
      if (!this.routeMap[path]) {
        throw new Error('path does not exist: ' + path);
      }

      var match;
      var newRoutes = [];

      // copy the routes excluding the route being removed
      for (var i = 0; i < this.routes.length; i++) {
        var route = this.routes[i];
        if (route.src !== path) {
          newRoutes.push(route);
        }
      }
      this.routes = newRoutes;
      delete this.routeMap[path];
    },

    match: function(pathname, startAt){
      var route = match(this.routes, pathname, startAt);
      if(route){
        route.fn = this.routeMap[route.route];
        route.next = this.match.bind(this, pathname, route.next)
      }
      return route;
    }
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.routes.match"></a>[function <span class="apidocSignatureSpan">routes.</span>match (routes, uri, startAt)](#apidoc.element.routes.match)
- description and source-code
```javascript
match = function (routes, uri, startAt) {
	var captures, i = startAt || 0;

	for (var len = routes.length; i < len; ++i) {
		var route = routes[i],
		    re = route.re,
		    keys = route.keys,
		    splats = [],
		    params = {};

		if (captures = uri.match(re)) {
			for (var j = 1, len = captures.length; j < len; ++j) {
				var key = keys[j-1],
					val = typeof captures[j] === 'string'
						? unescape(captures[j])
						: captures[j];
				if (key) {
					params[key] = val;
				} else {
					splats.push(val);
				}
			}
			return {
				params: params,
				splats: splats,
				route: route.src,
				next: i + 1
			};
		}
	}
}
```
- example usage
```shell
...
var Router = require('routes');
var router = Router();
var noop = function(){};

router.addRoute("/articles/:title?", noop);
router.addRoute("/:controller/:action/:id.:format?", noop);

console.log(router.match("/articles"));
console.log(router.match("/articles/never-gonna-let-you-down"));
console.log(router.match("/posts/show/1.json"));

'''

The output for 'router.match("/posts/show/1.json")' would be:
'''js
...
```

#### <a name="apidoc.element.routes.pathToRegExp"></a>[function <span class="apidocSignatureSpan">routes.</span>pathToRegExp (path, keys)](#apidoc.element.routes.pathToRegExp)
- description and source-code
```javascript
pathToRegExp = function (path, keys) {
	path = path
		.concat('/?')
		.replace(/\/\(/g, '(?:/')
		.replace(/(\/)?(\.)?:(\w+)(?:(\(.*?\)))?(\?)?|\*/g, function(_, slash, format, key, capture, optional){
			if (_ === "*"){
				keys.push(undefined);
				return _;
			}

			keys.push(key);
			slash = slash || '';
			return ''
				+ (optional ? '' : slash)
				+ '(?:'
				+ (optional ? slash : '')
				+ (format || '') + (capture || '([^/]+?)') + ')'
				+ (optional || '');
		})
		.replace(/([\/.])/g, '\\$1')
		.replace(/\*/g, '(.*)');
	return new RegExp('^' + path + '$', 'i');
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
