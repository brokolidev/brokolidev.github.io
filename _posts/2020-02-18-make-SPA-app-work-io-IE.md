---
title: "How to make the SPA app work on IE environment"
date: 2020-02-18 11:19:00 -0400
categories: [blog]
tags: [ blog, vue, laravel-mix, axios, ie, spa, laravel ]
---

I had set up the the SPA app with Vue JS(front-end) and Laravel(back-end)
It works great on any modern browsers but not on IE.

There were several problems.


### Axios does not work on IE

```js
# install
npm install es6-promise --save
```

```
// import it in main js file.
import 'es6-promise/auto'
```


### Object.assign doesn't work

```js
// import it in main js file.
npm install es6-promise --save
```

```
// import it in main js file.
if (typeof Object.assign != "function") {
    // Must be writable: true, enumerable: false, configurable: true
    Object.defineProperty(Object, "assign", {
        value: function assign(target, varArgs) {
            // .length of function is 2
            "use strict";
            if (target == null) {
                // TypeError if undefined or null
                throw new TypeError(
                    "Cannot convert undefined or null to object"
                );
            }

            var to = Object(target);

            for (var index = 1; index < arguments.length; index++) {
                var nextSource = arguments[index];

                if (nextSource != null) {
                    // Skip over if undefined or null
                    for (var nextKey in nextSource) {
                        // Avoid bugs when hasOwnProperty is shadowed
                        if (
                            Object.prototype.hasOwnProperty.call(
                                nextSource,
                                nextKey
                            )
                        ) {
                            to[nextKey] = nextSource[nextKey];
                        }
                    }
                }
            }
            return to;
        },
        writable: true,
        configurable: true
    });
}
```
