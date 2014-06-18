# 2bux

a better dom selection api

## What is it

It's a tiny little napkinfull of code that lets you omit jQuery without going insane. It's literally just [document.querySelector](https://developer.mozilla.org/en-US/docs/Web/API/document.querySelector) / [document.querySelectorAll](https://developer.mozilla.org/en-US/docs/Web/API/Document.querySelectorAll) but the latter returns an [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) instead of a [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) and both have an extra optional `context` argument.

## Why

* Becuase `document.querySelectorAll` is too long to type; I'd rather just type `$`
* Because `NodeList` doesn't have [forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
* Because I have become accustomed to terse code

Would you rather write this:

```javascript
var divsNodeList = document.querySelectorAll('div');
var divsArray = Array.prototype.slice.call(divsNodeList);
divsArray.forEach(function(div) {
  console.log(div.innerText);
});
```

or this?

```javascript
$$('div').forEach(function(div) {
  console.log(div.innerText);
});
```

## How big is it?

<1 kb unminified

## Installation

Using [Bower](http://bower.io/):

```
bower install 2bux
```

(you can also just grab the code [here](https://github.com/incompl/2bux/tree/master/src))

Supports both [AMD](http://requirejs.org/docs/whyamd.html) and browser globals using [UMD](https://github.com/umdjs/umd/blob/master/amdWeb.js).

The `$` and `$$` variables are placed in your global scope unless you are using AMD.

With AMD, to get both `$` and `$$`, you should do this:

```javascript
var $ = require("2bux"), $$ = $.$$;
```

## API

```javascript
$(selector, context); // returns a single element
```

```javascript
$$(selector, context); // returns an array of elements
```

* `selector` is a [CSS selector](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors)
* `context` is an optional DOM element (default `document`). Only children of `context` are queried. It's as if you had called `querySelector` or `querySelectorAll` on that DOM element rather than on the `document` object.

## Examples

```javascript
// get an element
var element = $('#special');
console.log(element.innerText);

// get an array of elements
var divs = $$('div');
console.log(divs.length);

// iterate over an array
$$('div').forEach(function(div) {
  console.log(div.innerText);
});

// get children of an element
var parent = $('#foo');
var children = $$('.bar', parent);
```

## Testing

* `npm install`
* `sudo npm install nodeunit -g`
* `nodeunit test`
