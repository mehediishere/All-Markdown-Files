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

## .on() & event handle

```
https://api.jquery.com/on/
```

### Display a paragraph's text in an alert when it is clicked:

```js
$( "p" ).on( "click", function() {
  alert( $( this ).text() );
});
```

### Pass data to the event handler, which is specified here by name:

```js
function myHandler( event ) {
  alert( event.data.foo );
}
$( "p" ).on( "click", { foo: "bar" }, myHandler );
```

### Cancel a form submit action and prevent the event from bubbling up by returning false:

```js
$( "form" ).on( "submit", false );
```

### Cancel only the default action by using .preventDefault().

```js
$( "form" ).on( "submit", function( event ) {
  event.preventDefault();
});
```

### Display each paragraph's text in an alert box whenever it is clicked:

```js
$( "body" ).on( "click", "p", function() {
  alert( $( this ).text() );
});
```

### Cancel a link's default action using the .preventDefault() method:

```js
$( "body" ).on( "click", "a", function( event ) {
  event.preventDefault();
});
```

### Attach multiple events—one on mouseenter and one on mouseleave to the same element:

```js
$( "#cart" ).on( "mouseenter mouseleave", function( event ) {
  $( this ).toggleClass( "active" );
});
```

```js
$( "#new-text-input" ).on( "keyup change", function( event ) {
  // ---
});
```

# AJAX

- page-1.php
- page-2.php

## page-1.php

```js
var id = $(this).attr("data-serial");
var user = $(this).attr("data-user");
var total = $(".total").val();
var location = $("#loc").val();

var request = $.ajax({
    method: "GET",
    url: "path/page-2.php",
    data: {
     // key: value
        id: id,
        name: user,
        total: total,
        loc: location,
        getData: "getData" // this is for `isset` use. like click a button for form submit/send or get data
    }
});

request.done(function(data) {
    var obj = JSON.parse(data);
    $("#un_id").text(obj["id2"]);
    $(".TotalAmount").text(obj["Amount"]);
    $("#grandTotal").text(obj["grand_total"]);
});
```

## page-2.php

```php
session_start();
require_once("../config/db.php");

if (isset($_GET['getData'])) {
    $id1 = $_GET['id'];
    $name1 = $_GET['name'];
    $total1 = $_GET['total'];
    $loc1 = $_GET['loc'];

    // ---------
    //     query / any calculation
    // ---------

    // Storing necessary data/value in an array
    $array = array("id2" => "value1", "Amount" => $total, "grand_total" => $amount_final['total']);

    // sending data with json encode
    echo json_encode($array);
    }
```