# FrontEnd-Development

## Get data attribute of Datalist
### HTML:
```html
<input list="browser" id="number">
<datalist id="browser">
    <option data-customvalue="Abc" value="Firefox">1</option>
    <option data-customvalue="Def" value="Chrome">2</option>
    <option data-customvalue="Ghi" value="Explorer">3</option>
</datalist>
```

### JS
```js
$('#number').on('input', function() {
    var value = $(this).val();
    alert($('#browser [value="' + value + '"]').data('customvalue'));
});
```
