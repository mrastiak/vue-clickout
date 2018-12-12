# vue-clickout

> Reusable clickout directive for reusable [Vue.js](https://github.com/vuejs/vue) components

[![npm version](https://img.shields.io/npm/v/vue-clickout.svg)](https://www.npmjs.com/package/vue-clickout)
[![CDNJS](https://img.shields.io/cdnjs/v/vue-clickout.svg)](https://cdnjs.com/libraries/vue-clickout)

## Overview

Sometimes you need to detect clicks **outside** of the element (to close a modal
window or hide a dropdown select). There is no native event for that, and Vue.js
does not cover you either. This is why `vue-clickout` exists. Please check out
the [demo](https://jsfiddle.net/simplesmiler/4w1cs8u3/150/) before reading further.

## Requirements

- vue: ^2.0.0

If you need a version for Vue 1, try `vue-clickout@1.0`.

## Install

From npm:

``` sh
$ npm install vue-clickout --save
```

From CDN, chose the one you prefer:

``` html
<script src="https://cdn.jsdelivr.net/npm/vue-clickout@2.2.2/dist/vue-clickout.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/vue-clickout/2.2.2/vue-clickout.min.js"></script>
<script src="https://cdn.rawgit.com/simplesmiler/vue-clickout/2.2.2/dist/vue-clickout.min.js"></script>
```

## Usage

1. Make the directive available to your component
2. Define a method to be called
3. Use the directive in the template

The recommended way is to use the mixin:

``` js
import { mixin as clickout } from 'vue-clickout';

export default {
  mixins: [ clickout ],
  template: '<p v-on-clickout="away">Click away</p>',
  methods: {
    away: function() {
      console.log('clicked away');
    },
  },
};
```

If mixin does not suit your needs, you can use the directive directly:

``` js
import { directive as onClickout } from 'vue-clickout';

export default {
  directives: {
    onClickout: onClickout,
  },
  template: '<p v-on-clickout="away">Click away</p>',
  methods: {
    away: function() {
      console.log('clicked away');
    },
  },
};
```

## Caveats

1. Pay attention to the letter case. `onClickout` turns into `v-on-clickout`,
   while `onClickAway` turns into `v-on-click-away`.
2. Prior to `vue@^2.0`, directive were able to accept statements.
   This is no longer the case. If you need to pass arguments, just do
   `v-on-clickout="() => away(arg1)"`.
3. There is a common issue with dropdowns (and modals) inside an element with
   `v-on-clickout`. Some UI libraries chose to implement these UI elements
   by attaching the DOM element directly to the body. This makes clicks on
   a dropped element trigger away handler. To combat that, you have to add
   an extra check in the handler, for where the event originated from.
   See #9 for an example.

## License

[MIT](https://opensource.org/licenses/MIT)
