## Form using ajax

### form
```html
<form id="my-form">
    @csrf
  <input type="text" name="email" id="email">
  <button type="submit">Submit</button>
</form>
<div id="form-messages"></div>

```


### ajax
```js
$(function() {
  $('#my-form').submit(function(event) {
    event.preventDefault(); // prevent the form from submitting normally

    var formData = $(this).serialize(); // get the form data

    $.ajax({
      type: 'POST',
      url: '/validate', // the Laravel route that will handle the validation
      data: formData,
      success: function(data) {
        // the validation was successful
        $('#form-messages').html('<div class="success">' + data.message + '</div>');
      },
      error: function(data) {
        // there were validation errors
        var errors = data.responseJSON.errors;
        var errorMsg = '<div class="error">';
        $.each(errors, function(key, value) {
          errorMsg += value + '<br>';
        });
        errorMsg += '</div>';
        $('#form-messages').html(errorMsg);
      }
    });
  });
});

```

### controller
```php
$validator = Validator::make($request->all(), [
    'email' => 'required|email|unique:users,email',
  ]);

  if ($validator->passes()) {
    // validation passed
    return response()->json(['message' => 'Validation passed.']);
  } else {
    // validation failed
    $errors = $validator->errors()->toArray();
    return response()->json(['errors' => $errors], 422);
  }
```
