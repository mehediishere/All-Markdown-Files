# jQuery - 

## CDN Link

> [https://releases.jquery.com/](https://releases.jquery.com/)

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
    method: "GET", // method GET/POST
    url: "path/page-2.php",
    data: {
     // key: value
        id: id,
        name: user,
        total: total,
        loc: location,
        getData: "getData" // (Optional) this is for `isset` use. like click a button for form submit/send or get data. 
                          // Since optional you can use other key for same purpose
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

## [Sum of values from different divs with the same class](https://stackoverflow.com/questions/7249757/sum-of-values-from-different-divs-with-the-same-class)
```html
<div class="totalprice">6.7</div>
<div class="totalprice">8.9</div>
<div class="totalprice">4.5</div>
```

```js
var sum = 0;
$('.totalprice').each(function()
{
    sum += parseFloat($(this).text());
});
alert(sum);
```

## [The Event in the DIV Not working after reload](https://stackoverflow.com/questions/35588911/the-event-in-the-div-not-working-after-reload) / After reload div click function not working solution

```js
 // On change qty field
 $('.field_item_qty').on( "change", function() {

 });
```
Basically your current version attaches to the dom object that exists at the time the page is loaded. When your div is rewritten it loses the event. By attaching to the parent with a selector for your element, you are saying to run this event for any child of mine that matches the selector, now or in the future.

**Solution:**

```js
// On change qty field
$(document).on("change", ".field_item_qty", function() {

});
```

## [Preview an image before it is uploaded](https://stackoverflow.com/questions/4459379/preview-an-image-before-it-is-uploaded)

```html
<input type='file' onchange="readURL(this);" /> 
<img id="ShowImage" src="#" />
```

```js
 function readURL(input) {
    if (input.files && input.files[0]) {
        var reader = new FileReader();

        reader.onload = function (e) {
            $('#ShowImage')
                .attr('src', e.target.result)
                .width(150)
                .height(200);
        };

        reader.readAsDataURL(input.files[0]);
    }
}
```

## Reload only a div/section

Note: <code>+ " #cart-icon-count"</code> here space is mendatory inside of double quotation

```js
$("#cart-icon-count").load(window.location.href + " #cart-icon-count");
```

## Add text / elements into another element & fadeout after few seconds

Ex. Coupon redeemtion / expire message

```js
$('.coupon-msg').html('<label class="fd"><span class="text-success"><i class="fas fa-check"></i> Coupon successfully redeemed.</span></label>').fadeOut(2000,function(){ $('.fd').remove(); $('.coupon-msg').show(); });
```
