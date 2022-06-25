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

## Option in a Select tag carry multiple values
### HTML
```html
<form name="car_form" method="post" action="doublevalue_action.php">
        <select name="car" id="car">
                <option value="">Select Car</option>
                <option value="BMW|Red">Red BMW</option>
                <option value="Mercedes|Black">Black Mercedes</option>
        </select>
        <input type="submit" name="submit" id="submit" value="submit">
</form>
```

### PHP
```php
<?php
    $result = $_POST['car'];
    $result_explode = explode('|', $result);
    echo "Model: ". $result_explode[0]."<br />";
    echo "Colour: ". $result_explode[1]."<br />";
?>
```
