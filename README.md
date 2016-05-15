[![NPM Version](https://img.shields.io/npm/v/gulp-inline-source-from.svg?style=flat)](https://www.npmjs.com/package/gulp-inline-source-from)

# gulp-inline-source-from

Inline tags that contain the `from` attribute. Supports `<script>`, `<link>`, and especialy `<style>`.
This module was created because I wanted to use CSS preprocessors like LESS or SASS for my Polymer project and I needed a way to inline my compiled styles into my source *.html over and over. With this module you can place `<style from='./path/to.css'>` inside your html souce file and when you run the gulp task it it will pickup the file referenced in from attribute and inline it inside the element, while preserving the from attribute.
This module is forked and modified from excelent module [inline-source](https://www.npmjs.com/package/inline-source) and it's gulp variant [gulp-inline-source](https://www.npmjs.com/package/gulp-inline-source) I make no claim to their code and I thak them very much.

## How it works

```html
<!-- located at /elements/my-element.html -->
<dom-module is="my-element">
    <!-- inline ./my-element.css generated from ./my-element.less -->
    <style from="./my-element.css"></style>
  <template>
  </template>
  <!-- inline ./my-element.js generated from ./my-element.ts -->
  <script from="./my-element.js"></script>
</dom-module>
```

```css
/* located at ./my-element.css */

:host {
  color: blue;
}
```

```js
// located at ./my-element.js

Polymer({
      is: 'my-element'
    });
```

Output:
```html
<!-- located at /elements/my-element.html -->
<dom-module is="my-element">
    <!-- inline ./my-element.css generated from ./my-element.less -->
    <style from="./my-element.css">
      :host {
        color: blue;
      }
    </style>
  <template>
  </template>
  <!-- inline ./my-element.js generated from ./my-element.ts -->
  <script from="./my-element.js">
    Polymer({
      is: 'my-element'
    });
  </script>
</dom-module>
```

## Install

```bash
$ npm install gulp-inline-source-from --save-dev
```

## Usage

```javascript
var gulp = require('gulp');
var inlinefrom = require('gulp-inline-source-from');

gulp.task('inline', function () {
    return gulp.src("./elements/**/*.html").pipe(inlinefrom()).pipe(gulp.dest("./out/"));
    //return gulp.src("./elements/**/*.html").pipe(inline()).pipe(gulp.dest("./elements/")); //WARNING this will starts to overwrite your files, use with causion when you are confident it works as you expect it to.
});
```

Optionally, you can provide [some options](https://github.com/popeindustries/inline-source#usage) through an options object, BUT BE WARNED: I have made some braking changes to the original code, so some functionality is lost.
