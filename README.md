## What is this?
This is a starter kit for `AngularJS 1.5.x` & `ES6` application.

## Installation and usage
### Prerequisites

Make sure you have globally installed latest versions of [NodeJS](https://nodejs.org):
* Node 4+
* NPM 3+

Make sure you have globally installed latest versions of such NPM modules:
* Gulp 4
* webpack

### Install
Run `npm install` to download all dependencies

### Usage - Development
Run `npm run serve` to start watcher and local server. Follow console messages.

In case of error, make sure you have latest version of Gulp installed


### Usage - Production
Run `npm run build` to compile and minify all files. Find them in `/dist` folder.

## AngularJS 1.x & ES6 & Module bundler (Webpack):

In this section we'll described some specific techniques using the combination
of `AngularJS 1.x` and `ES6` and `Webpack (or any other module bundler)`
 
### Templates
#### 1. using absolute path to html file
```js
let myComponent = {
    templateUrl: 'app/components/myComponent/myComponent.html'
}
```

in this case the `buld` task will place all templates into `$templateCache`

#### 2. importing html file and inserting inline
```js
import template from './footer.html'

let myComponent = {
    template: template
}
```

in this case template will be paste HTML inline. To make [Webpack][wp] import `html` files we've added a 
[`html-loader`](https://github.com/webpack/html-loader). And here's how Webpack's
configuration would look like:
```js
module: {
    loaders: [
        // ...
        {
            test: /\.html$/,
            loader: "html"
        },
        // ...
```

---

A recommendation is to use second variant. If you are sure that first variant is not used anywhere then
you may also remove Gulp's `partials` task in order to get rid of unused templates.


### Modules
#### External modules

```js
import ngAnimate from 'angular-animate'   // variant 1
import 'angular-ui-router'                // variant 2

angular.module('myApp', [ngAnimate, 'ui.router'])
```

Using **variant 2** you'll need to know the exact name of the imported module (e.g.`ui.router`) 
to include it as a dependency to your application. 
**variant 1** doesn't need that, you may use a variable here.
 
**variant 1** is recommended

#### Internal modules

`child-module.js`:

```js
export const childModule = 'childModule';

angular.module(childModule, [])
```

`parent-module.js`:

```js
import {childModule} from './child-module';

angular.module('myApp', [ childModule ])
```




[wp]: https://webpack.github.io/