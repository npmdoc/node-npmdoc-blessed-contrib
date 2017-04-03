# api documentation for  [blessed-contrib (v4.7.5)](https://github.com/yaronn/blessed-contrib#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-blessed-contrib.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-blessed-contrib) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-blessed-contrib.svg)](https://travis-ci.org/npmdoc/node-npmdoc-blessed-contrib)
#### Build dashboards (or any other application) using ascii/ansi art and javascript.

[![NPM](https://nodei.co/npm/blessed-contrib.png?downloads=true)](https://www.npmjs.com/package/blessed-contrib)

[![apidoc](https://npmdoc.github.io/node-npmdoc-blessed-contrib/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-blessed-contrib_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-blessed-contrib/build..beta..travis-ci.org/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-blessed-contrib/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-blessed-contrib/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Yaron Naveh",
        "url": "yaronn01@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/yaronn/blessed-contrib/issues"
    },
    "dependencies": {
        "ansi-term": ">=0.0.2",
        "chalk": "^1.1.0",
        "drawille-canvas-blessed-contrib": ">=0.1.3",
        "lodash": ">=3.0.0",
        "map-canvas": ">=0.1.5",
        "marked": "^0.3.3",
        "marked-terminal": "^1.5.0",
        "memory-streams": "^0.1.0",
        "memorystream": "^0.3.1",
        "picture-tube": "0.0.4",
        "request": "^2.53.0",
        "sparkline": "^0.1.1",
        "strip-ansi": "^3.0.0",
        "term-canvas": "0.0.5",
        "x256": ">=0.0.1"
    },
    "description": "Build dashboards (or any other application) using ascii/ansi art and javascript.",
    "devDependencies": {
        "blessed": "0.1.54",
        "colors": "^1.1.2"
    },
    "directories": {},
    "dist": {
        "shasum": "4fae074bbdc0a3af59671fcf54361e9c011576b3",
        "tarball": "https://registry.npmjs.org/blessed-contrib/-/blessed-contrib-4.7.5.tgz"
    },
    "gitHead": "443af80954899fb62fe86b32b799708b0dee60bc",
    "homepage": "https://github.com/yaronn/blessed-contrib#readme",
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "yaron",
            "email": "yaronn01@gmail.com"
        }
    ],
    "name": "blessed-contrib",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/yaronn/blessed-contrib.git"
    },
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "version": "4.7.5"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module blessed-contrib](#apidoc.module.blessed-contrib)
1.  object <span class="apidocSignatureSpan">blessed-contrib.</span>utils

#### [module blessed-contrib.utils](#apidoc.module.blessed-contrib.utils)
1.  [function <span class="apidocSignatureSpan">blessed-contrib.utils.</span>MergeRecursive (obj1, obj2)](#apidoc.element.blessed-contrib.utils.MergeRecursive)
1.  [function <span class="apidocSignatureSpan">blessed-contrib.utils.</span>abbreviateNumber (value)](#apidoc.element.blessed-contrib.utils.abbreviateNumber)
1.  [function <span class="apidocSignatureSpan">blessed-contrib.utils.</span>getColorCode (color)](#apidoc.element.blessed-contrib.utils.getColorCode)
1.  [function <span class="apidocSignatureSpan">blessed-contrib.utils.</span>getTypeName (thing)](#apidoc.element.blessed-contrib.utils.getTypeName)



# <a name="apidoc.module.blessed-contrib"></a>[module blessed-contrib](#apidoc.module.blessed-contrib)



# <a name="apidoc.module.blessed-contrib.utils"></a>[module blessed-contrib.utils](#apidoc.module.blessed-contrib.utils)

#### <a name="apidoc.element.blessed-contrib.utils.MergeRecursive"></a>[function <span class="apidocSignatureSpan">blessed-contrib.utils.</span>MergeRecursive (obj1, obj2)](#apidoc.element.blessed-contrib.utils.MergeRecursive)
- description and source-code
```javascript
function MergeRecursive(obj1, obj2) {

  if (obj1==null) return obj2
  if (obj2==null) return obj1

  for (var p in obj2) {
    try {
      // property in destination object set; update its value
      if ( obj2[p].constructor==Object ) {
        obj1[p] = MergeRecursive(obj1[p], obj2[p]);

      } else {
        obj1[p] = obj2[p];

      }

    } catch(e) {
      // property in destination object not set; create it and set its value
      obj1[p] = obj2[p];

    }
  }

  return obj1;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.blessed-contrib.utils.abbreviateNumber"></a>[function <span class="apidocSignatureSpan">blessed-contrib.utils.</span>abbreviateNumber (value)](#apidoc.element.blessed-contrib.utils.abbreviateNumber)
- description and source-code
```javascript
function abbreviateNumber(value) {
    var newValue = value;
    if (value >= 1000) {
        var suffixes = ["", "k", "m", "b","t"];
        var suffixNum = Math.floor( (""+value).length/3 );
        var shortValue = '';
        for (var precision = 2; precision >= 1; precision--) {
            shortValue = parseFloat( (suffixNum != 0 ? (value / Math.pow(1000,suffixNum) ) : value).toPrecision(precision));
            var dotLessShortValue = (shortValue + '').replace(/[^a-zA-Z 0-9]+/g,'');
            if (dotLessShortValue.length <= 2) { break; }
        }
        if (shortValue % 1 != 0)  shortNum = shortValue.toFixed(1);
            newValue = shortValue+suffixes[suffixNum];
        }
    return newValue;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.blessed-contrib.utils.getColorCode"></a>[function <span class="apidocSignatureSpan">blessed-contrib.utils.</span>getColorCode (color)](#apidoc.element.blessed-contrib.utils.getColorCode)
- description and source-code
```javascript
function getColorCode(color) {
    if (Array.isArray(color) && color.length == 3)
    {
        return x256(color[0],color[1],color[2]);
    }
    else
    {
      return color;
    }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.blessed-contrib.utils.getTypeName"></a>[function <span class="apidocSignatureSpan">blessed-contrib.utils.</span>getTypeName (thing)](#apidoc.element.blessed-contrib.utils.getTypeName)
- description and source-code
```javascript
function getTypeName(thing){
    if(thing===null)return "[object Null]"; // special case
    return Object.prototype.toString.call(thing);
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
