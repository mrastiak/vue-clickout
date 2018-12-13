# vue-clickout

> Reusable clickout directive for reusable [Vue.js](https://github.com/vuejs/vue) components. forked from [vue-clickaway](https://github.com/simplesmiler/vue-clickaway)

[![npm version](https://img.shields.io/npm/v/vue-clickout.svg)](https://www.npmjs.com/package/vue-clickout)

## Overview

Sometimes you need to detect clicks **outside** of the element (to close a modal
window or hide a dropdown select). There is no native event for that, and Vue.js
does not cover you either. This is why `vue-clickout` exists.

## Why not [vue-clickaway](https://github.com/simplesmiler/vue-clickaway)?

This library is forked from [vue-clickaway](https://github.com/simplesmiler/vue-clickaway). The main reason for creating a separate library is lack of some features in the vue-clickaway. for example `stop` modifier for `stopPropagation` support and `capture` for capturing support.

## Requirements

- vue: ^2.0.0

## Install

```sh
$ npm install vue-clickout --save
```

## Usage

1. Make the directive available to your component
2. Define a method to be called
3. Use the directive in the template

The recommended way is to use the mixin:

```js
import { mixin as clickout } from 'vue-clickout'

export default {
  mixins: [clickout],
  template: '<p v-on-clickout="out">Click out</p>',
  methods: {
    out: function() {
      console.log('clicked out')
    }
  }
}
```

If mixin does not suit your needs, you can use the directive directly:

```js
import { directive as onClickout } from 'vue-clickout'

export default {
  directives: {
    onClickout: onClickout
  },
  template: '<p v-on-clickout="out">Click out</p>',
  methods: {
    out: function() {
      console.log('clicked out')
    }
  }
}
```

## Caveats

1. Pay attention to the letter case. `onClickout` turns into `v-on-clickout`,
   while `onClickOut` turns into `v-on-click-out`.
2. Prior to `vue@^2.0`, directive were able to accept statements.
   This is no longer the case. If you need to pass arguments, just do
   `v-on-clickout="() => out(arg1)"`.
3. There is a common issue with dropdowns (and modals) inside an element with
   `v-on-clickout`. Some UI libraries chose to implement these UI elements
   by attaching the DOM element directly to the body. This makes clicks on
   a dropped element trigger away handler. To combat that, you have to add
   an extra check in the handler, for where the event originated from.
   See #9 for an example.

## License

[MIT](https://opensource.org/licenses/MIT)
