# Handle css and template

---

Css and html template are significant parts in front-end development, and spm is just good for it.

## Css

The spm package could be a pure css package, use `main` and `output` to specify endpoint files.

For Example, there is a `main-style` package for our site layout:

```
button.css
tip.css
index.css
package.json
```

```json
{
  "name": "main-style",
  "version": "1.0.0",
  "spm": {
    "dependencies": {
      "normalize.css": "3.0.1"
    },
    "main": "index.css"
  }
}
```

Simply import files and other packages  by a standard `@import`.

```
/* index.css */
@import (css) '~normalize.css';

@import './button.css';
@import './tip.css';
```

[alice-button](https://github.com/aliceui/button) is a nice example as well.

You can also require css package in js file, just like js package but without exports.

```
require('main-style');
var moment = require('moment');
```


## Template

Fisrtly, write your template in file, named it as `*.html` or `*.tpl` or `*.handlebars`.

**Realtime Compile**

```html
<!-- defalut.tpl -->
<div>
  <span>{{name}}</span>
  <span>{{content}}</span>
</div>
```

Then require it in js file.

```js

var Handlebars =  require('handlebars');
var source = require('./tpl/tpl.tpl');

var template = Handlebars.default.compile(source);
var result = template({
  name: 'alex',
  content: 'content'
});

console.log(result);
```

*Precompile**

```html
<!-- defalut.handlebars -->
<div>
  <span>{{name}}</span>
  <span>{{content}}</span>
</div>
```

Then require it in js file.

```js

var source = require('./defalut.handlebars');
var result = source({
  name: 'alex',
  content: 'content'
});
console.log(result);
```



