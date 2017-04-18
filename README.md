# npmdoc-routes

#### api documentation for  [routes (v2.1.0)](https://github.com/aaronblohowiak/routes.js)  [![npm package](https://img.shields.io/npm/v/npmdoc-routes.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-routes) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-routes.svg)](https://travis-ci.org/npmdoc/node-npmdoc-routes)

#### Minimalist route matching for javascript

[![NPM](https://nodei.co/npm/routes.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/routes)

- [https://npmdoc.github.io/node-npmdoc-routes/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-routes/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-routes/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-routes/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-routes/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-routes/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Aaron Blohowiak",
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
            "name": "aaronblohowiak"
        },
        {
            "name": "raynos"
        }
    ],
    "name": "routes",
    "optionalDependencies": {},
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



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
