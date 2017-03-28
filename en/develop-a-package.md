# Develop A Package

---

You can follow the steps to develop a package using [spm](https://github.com/spmjs/spm).

```
$ spm --version
3.6.0
```

Make sure that spm@3.6.0 is installed.

## init

```bash
$ mkdir now && cd now
$ spm init
```

```
Creating a spm package:
[?] Package name: (now)
[?] Version: (1.0.0)
[?] Description: hello world
[?] Author: pigcan <jiangjay818@gmail.com>

Initialize a spm package Succeccfully!
```

Then you have a package named `now`.

## Install dependencies

Install default devDependencies first.

```bash
$ spm install
```

We need [moment](http://momentjs.com) as a dependency which can be found [here](http://spmjs.io/package/moment).

```bash
$ spm install moment --save
```

## Code and Debug

Edit `index.js` as follow, just like nodejs.

```javascript
// require module in spm.dependencies
var moment = require('moment');

// require relative file in you project
// var util = require('./util');

var now = moment().format('MMMM Do YYYY, h:mm:ss a');
module.exports = now;
```

Then edit `examples/index.md`:

<pre>
# Demo

---

## Normal usage

````javascript
var now = require('../index');
console.log(now);
````
</pre>


Run `spm doc` to start a documentation service at `127.0.0.1:8000` .

```bash
$ spm doc
```

Open [http://127.0.0.1:8000/examples/](http://127.0.0.1:8000/examples/) in browser to see the result.

Except using three &#96; in Markdown file, you can also use four &#96; to wrap your code.

It is a special rule that highlights your code and inserts it to a document page as a script block so they can be excuted at the same time. This is very useful for debugging your demo and writing beautiful documentation.

If you want to insert an iframe in your demo, make your code to `iframe` type.

<pre>
````iframe:600
I am in an iframe of 600px high
````
</pre>


> If you don't want to debug your code by `spm doc`, you can try [spm-webpack-server](https://github.com/spmjs/spm-webpack-server) to debug `CommonJS` modules in development.

## Add Test Case

Edit test file at `tests/now-spec.js`. We introduce a default assert solution [expect.js](http://spmjs.io/package/expect.js).

```javascript
var expect = require('expect.js');
var now = require('../index');

describe('now', function() {

  it('normal usage', function() {
    expect(now).to.be.a('string');  // add this
  });

});
```

See tests result.

```bash
$ spm test
```

You can also open [http://127.0.0.1:8000/tests/runner.html](http://127.0.0.1:8000/tests/runner.html) in browser.

## Publish

Now you have a great package with wonderful functions and complete test cases, which you can publish to [spmjs.io](http://spmjs.io/).

```bash
$ spm publish
```

First you should run `spm login` to get permission, otherwise it will propmt the authorization problem. 

```bash
$ spm login
```

`username` is the name of your github account, and `authkey` can be found at http://spmjs.io/account after signing in.

> The package `now` is published by me, of course. You should change other name and retry.

## Documentation

spmjs.io can host your package's documentation. What all you need to do is editing `README.md` and `examples` folder, preview it by `spm doc watch`, then publish it to spmjs.io.

```bash
$ spm doc publish
```

The documentation url is `http://docs.spmjs.io/{{name}}/` for the latest version and `http://docs.spmjs.io/{{name}}/{{version}}/` for each versions.

For example, http://docs.spmjs.io/now/.

## Build

```bash
$ spm build
```

This command will build the files indicated by `spm.main` and `spm.output` fields to `dist` folder. The `spm.build` would be executed as arguments.

The default build result is a package which can be deployed at cdn and then used. For example,

**In your html**
```html
<script>
  var now = require('now');
  console.log(now);
</script>
```
**In your project package.json**

```javascript
{
    "name": "Project-Name",
    "spm": {
        "output": ["index.js"],
        "dependencies": {
            "now": "1.0.0"
        }
    },
    "devDependencies": {
        "spm": "~3.6.0"
    },
    "scripts": {
        "build": "spm build"
    }
}
```
## Congratulation

Now you learn how to develop a package using spm, welcome to publish your packages here!
