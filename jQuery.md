# jQuery - 

## CDN Link
```
https://releases.jquery.com/
```
Version 3.6.0 (minified)
```js
<script src="https://code.jquery.com/jquery-3.6.0.min.js" integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4=" crossorigin="anonymous"></script>
```

## Making DOM Ready

When the `document` is `ready`, execute this function `...`
```js
$(document).ready(function() { 

 });
```
A commonly used shorthand version (behaves the same as the above)
```js
$(function() { 

 });
```

## Set the <em>TEXT</em> inside the selected element

### HTML
```html
<p id="hello">Some random text</p>
```
### JS
```js
$(document).ready(function () {
    $('#hello').text('Hello, World!');
});
```
### Output
```
Hello, World!
```

<hr>

### HTML
```html
<p class="hello">Some random text</p>
```
### JS
```js
$(document).ready(function () {
    $('.hello').text('Hello, World!');
});
```
### Output
```
Hello, World!
```

<hr>

Here h1 & p both of their text will show one same this, one time in one line

### HTML
```html
<div class="hello">
    <h1>Random header</h1>
    <p>Some random text</p>
</div>
```
### JS
```js
$(document).ready(function () {
    $('.hello').text('Hello, World!');
});
```
### Output
```
Hello, World!
```

<hr>

### HTML
```html
<div class="hello">
    <h1 class="hello2">Random header</h1>
    <p>Some random text</p>
</div>
```
### JS
```js
$(document).ready(function () {
    $('.hello .hello2').text('Random header changed');
});
```
### Output
```
Random header changed
Some random text
```

## Appending an element to a container

