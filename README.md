# vueify

> Browserify transform for Vue.js components

This transform allows you to write your components in this format:

``` html
// app.vue
<style>
  .red {
    color: #f00;
  }
</style>

<template>
  <h1 class="red">{{msg}}</h1>
</template>

<script>
  module.exports = {
    data: function () {
      return {
        msg: 'Hello world!'
      }
    }
  }
</script>
```

You can also mix preprocessor languages in the component file:

``` html
// app.vue
<style lang="stylus">
.red
  color #f00
</style>

<template lang="jade">
h1(class="red") {{msg}}
</template>

<script lang="coffee">
module.exports =
  data: ->
    msg: 'Hello world!'
</script>
```

Under the hood, the transform will:

- extract the styles, compile them and insert them with the `insert-css` module.
- extract the template, compile it and add it to your exported options.

You can `require()` other stuff in the `<script>` as usual. Note that for CSS-preprocessor @imports, the path should be relative to your project root directory.

## Usage

``` bash
npm install vueify --save-dev
browserify -t vueify -e src/main.js -o build/build.js
```

And this is all you need to do in your main entry file:

``` js
// main.js
var Vue = require('vue')
var appOptions = require('./app.vue')
var app = new Vue(appOptions).$mount('#app')
```

## Enabling Pre-Processors

You need to install the corresponding node modules to enable the compilation. e.g. to get stylus compiled in your Vue components, do `npm install stylus --save-dev`.

Currently supported preprocessors are:

- stylus
- less
- scss (via `node-sass`)
- jade
- coffee-script

And here's a SublimeText syntax definition for enabling language hihglighting/support in these embbeded code blocks: https://gist.github.com/yyx990803/9194f92d96546cebd033

## Example

For an example setup, see [vuejs/vueify-example](https://github.com/vuejs/vueify-example).

---

If you use Webpack, there's also [vue-loader](https://github.com/vuejs/vue-loader) that does the same thing.