# vue-signature

> A electronic signature component by Vue.js

> Forked from https://github.com/WangShayne/vue-signature

## Changes from original
* fromDataUrl method renamed to load
* template linted with B2B for vue-2
* added button classes for bootstrap-vue
* THATS IT! nothing big, just wanted to make it work for my use-case



## Reference and Thanks
[signature_pad](https://github.com/szimek/signature_pad)

## API
---
#### Props
> w,h need units,like 100px or 100%

| name          |     type      |           default         |       description             |
|:-------------:|:-------------:|:-------------------------:|   :-----------------:         |
| sigOption     | `Obeject`     | {penColor:"rgb(0, 0, 0)", backgroundColor:"rgb(255,255,255)"} |     penColor, backgroundColor  |
|        w      | `String`      |         "100%"            |parent container width  |
|        h      | `String`      |         "100%"            |parent container height |
|  clearOnResize  | `Boolean`     |          false          |Canvas is cleared on window resize|


#### Methods
| name              |  params                                       | description  |
| :-------------:   |:-------------:                                |:-------------:|
| save              | 			()/("image/jpeg")/("image/svg+xml") | save image as PNG/JPEG/SVG |
| clear             |                                   			| clear canvas |
| isEmpty           |                                   			| Returns true if canvas is empty, otherwise returns false |
| undo             |                                   			| remove the last dot or line |
| addWaterMark      |           {} // check Usage addWaterMark    | addWaterMark
| load      |          (url)    | Draws signature image from data URL.


## Usage
---

``` 
npm install vue-signature 
```

main.js

```
import vueSignature from "vue-signature"
Vue.use(vueSignature)
```
A.vue

```
<template>
    <div id='app'>
        <vueSignature ref="signature" :sigOption="option" :w="'100%'" :h="'200px'"></vueSignature>
        <!-- <vueSignature ref="signature1" :sigOption="option"></vueSignature> -->
        <button class='float-right ml-2 btn btn-info' @click="addWaterMark">addWaterMark</button>
        <button class='float-right ml-2 btn btn-warning' @click="undo">Undo</button>
        <button class='float-right ml-2 btn btn-danger' @click="clear">Clear</button>
        <button class='float-right ml-2 btn btn-success' @click="save">Save</button>
    </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      option: {
        penColor: 'rgb(0, 0, 0)',
        backgroundColor: 'rgb(255,255,255)',
      },
    };
  },
  methods: {
    save() {
      const png = this.$refs.signature.save();
      const jpeg = this.$refs.signature.save('image/jpeg');
      const svg = this.$refs.signature.save('image/svg+xml');
      console.log(png);
      console.log(jpeg);
      console.log(svg);
    },
    clear() {
      this.$refs.signature.clear();
    },
    undo() {
      this.$refs.signature.undo();
    },
    addWaterMark() {
      this.$refs.signature.addWaterMark({
        text: 'berryTechnics',          // watermark text, > default ''
        font: '20px Arial',         // mark font, > default '20px sans-serif'
        style: 'all',               // fillText and strokeText,  'all'/'stroke'/'fill', > default 'fill
        fillStyle: 'red',           // fillcolor, > default '#333'
        strokeStyle: 'blue', // strokecolor, > default '#333'
        x: 100,                     // fill positionX, > default 20
        y: 200,                     // fill positionY, > default 20
        sx: 100,                    // stroke positionX, > default 40
        sy: 200,                     // stroke positionY, > default 40
      });
    },
    load(url) {
      this.$refs.signature.fromDataURL(url);
    },
  },
};
</script>

```


## License
---
Released under the [MIT License](https://opensource.org/licenses/MIT).
