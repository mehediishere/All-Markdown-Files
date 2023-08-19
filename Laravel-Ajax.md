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

## Ajax with Datatable

### Form

```html
<div class="table-responsive">
    <table class="table table-bordered table-striped" id="sell_quantity_table_report">
        <thead>
        <tr>
            <th>SL</th>
            <th>Product</th>
            <th>Quantity</th>
        </tr>
        </thead>
        <tbod>

        </tbod>
    </table>
</div>
```

### Ajax

```js
$(document).ready(function() {
    if($('#tr_date_range').length == 1){
        $('#tr_date_range').daterangepicker({
            ranges: ranges,
            autoUpdateInput: false,
            startDate: moment().startOf('month'),
            endDate: moment().endOf('month'),
            locale: {
                format: moment_date_format
            }
        });
        $('#tr_date_range').on('apply.daterangepicker', function(ev, picker) {
            $(this).val(picker.startDate.format(moment_date_format) + ' ~ ' + picker.endDate.format(moment_date_format));
            table_report.ajax.reload();
        });
    
        $('#tr_date_range').on('cancel.daterangepicker', function(ev, picker) {
            $(this).val('');
            table_report.ajax.reload();
        });
    }
    
    table_report = $('#sell_quantity_table_report').DataTable({
        "ajax": {
            "url": "/reports/sell-quantity-report",
            "data": function ( d ) {
                d.location_id = $('#tr_location_id').val();
                d.start_date = $('#tr_date_range').data('daterangepicker').startDate.format('YYYY-MM-DD');
                d.end_date = $('#tr_date_range').data('daterangepicker').endDate.format('YYYY-MM-DD');
            }
        },
        processing: true,
        serverSide: false,
        columns: [
            {data: 'iteration', name: 'iteration'},
            {data: 'product', name: 'product'},
            {data: 'quantity', name: 'quantity'},
        ],
        "fnDrawCallback": function (oSettings) {
            __currency_convert_recursively($('#sell_quantity_table_report'));
        }
    });
    
    //Customer Group report filter
    $('select#tr_location_id, #tr_date_range').change( function(){
        table_report.ajax.reload();
    });
});
```

### Controller
```php
public function sellQuantityReport(Request $request)
{
    if ($request->ajax()) {
        $start_date = $request->get('start_date');
        $end_date = $request->get('end_date');

        $transactions = TransactionSellLine::select('id', 'product_id', 'variation_id', DB::raw('SUM(quantity) as quantity'))
            ->with('product:id,name,image', 'variations:id,name')
            ->whereBetween('created_at', [$start_date, $end_date])
            ->groupBy('variation_id')
            ->get();

        $pr = [];
        $iteration = 1;
        foreach ($transactions as $transaction) {
            $product = $transaction->product['name'] . ($transaction->variations['name'] != "DUMMY" ? " (" .$transaction->variations['name'] . ")" : '');
            $quantity = $transaction->quantity;

            $pr[] = [
                "iteration" => $iteration++,
                "product" => $product,
                "quantity" => $quantity,
            ];
        }

        $response = [
            "data" => $pr,
        ];

        return response()->json($response);
    }

    return view('report.sell_qty_report');
}
```
