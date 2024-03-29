<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://github.com/mehediishere/All-Markdown-Files/blob/93df229ed473c6c71358163a3623e2dcd49796db/Images/lara-core.jpg" width="100%"></a></p>

<p align="center">
<img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version">
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

# Laravel Common Commands

## Navigation
<details>
<summary>Open Navigation</summary>
  <ul>
    <li><a href="#Start-server">Start server</a></li>
    <li><a href="#Route">Route</a></li>
    <li><a href="#Adding-CSS-or-JS-links">Adding CSS or JS links</a></li>
    <li><a href="#Create-model-controller-migration">Create model, controller, migration</a></li>
    <li><a href="#Recomend-file-naming-style">Recomend file naming style</a></li>
    <li><a href="#Create-model-controller-migration-from-single-command">Create model, controller, migration from single command</a></li>
    <li><a href="#Update-specific-table">Update Specific Table</a></li>
    <li><a href="#Write-php-code">Write php code</a></li>
    <li><a href="#Passing-a-variable-in-view">Passing a variable in view</a></li>
    <li><a href="#Toggle-Navbar-active-class">Toggle Navbar active class</a></li>
    <li><a href="#How-to-display-html-data-post-in-page">How to display html data post in page?</a></li>
    <li><a href="#Query">Query</a></li>
    <li><a href="#Show-html-data-with-limited-words">Show html data with limited words</a></li>
    <li><a href="#Share-variable-across-all-controller-and-view">Share variable across all controller and view</a></li>
    <li><a href="#Cookie">Cookie</a></li>
    <li><a href="#Passing-parameters-to-your-controller-using-anchor-tag">Passing one/two parameters to your controller using anchor tag</a></li>
    <li><a href="#Ajax">Ajax</a></li>
    <li><a href="#Faker">Faker</a></li>
  </ul>
</details>

<br>

## Start server

```
php artisan serve
```

## Route

There has six type of Route method

|Method   | Usage  |
|---|---|
| GET  | When you have to fetch some data/send some data to a page, you may use this method. |
| POST  | When you want to insert data to database, then you may use this.  |
| PUT  | When you want to update datas to database, you may use this.  |
| PATCH  | When you want to update a single field in database, you may use this.  |
| DELETE  | When you want to update a single field in database, you may use this. |
| OPTIONS  |   |

Note : It's not like for this particular action, you have to use this method. You can use any method for any action you feel right/confortable.

```php
Route::get('/greeting', function () {
    return 'Hello World';
});
```

> ### The [any](https://www.educative.io/answers/what-are-laravel-basic-routing-and-available-router-methods) method

Laravel provides a fluent way to respond to any HTTP request using the **any()** method like below. This method will respond to any HTTP request directed to that url.

```php
Route::any('/', function () {
    //
});
```

> ### The [match](https://www.educative.io/answers/what-are-laravel-basic-routing-and-available-router-methods) method


We might want to filter the HTTP method that we wish to respond to, so we use the **match()** method.

```php
Route::match(['get', 'post'], '/', function () {
    //
});
```

### Check All Used/Currently available (in project) route list

```php
php artisan r:l
```

> ## Url

Recomended way:

```html
<a herf="{{ route('about.page') }}">About</a>
```

```php
Route::controller(DemoController::class)->group(function(){
    Route::get('/about', 'aboutMethod')->name('about.page');
    Route::get('/contact', 'contactMethod')->name('contact.page');
});
```

Another way:

```html
<a herf="{{ url('/about') }}">About</a>
```

```php
Route::controller(DemoController::class)->group(function(){
    Route::get('/about', 'aboutMethod');
    Route::get('/contact', 'contactMethod');
});
```

> (Laravel v8 - way):

```html
<a herf="{{ url('/about') }}">About</a>
```

```php
Route::get('/about', [DemoController::class, 'aboutMethod']);
Route::get('/contact', [DemoController::class, 'contactMethod']);
```

## Adding CSS or JS links

If you want use css/js files from local, place files in public folder. Then,

```css
<link rel="stylesheet" href="{{ asset('css/bootstrap.min.css') }}">
```
<small>Here `bootstrap.min.css` file is in css folder. That `css` folder inside of `public` folder.</small>

## Create model, controller, migration

### Recomend file naming style

Lets say we need an `Admin` model, controller & table

|Model | Controller | Table / Migration |
|---|---|---|
| Admin | AdminController | admins |

> Migration
```php
php artisan make:migration create_admins_table
```
<small>Note: (Not necessary to follow. Just many dev do so) A common practice is to have `migration` name in `plural` form</small>

> Controller
```php
php artisan make:controller AdminController
```
<small>Note: (Not necessary to follow. Just many dev do so) A common practice is to have `controller` name in `camelcase` style and end with `controller` word</small>

> Model
```php
php artisan make:model Admin
```
<small>Note: (Not necessary to follow. Just many dev do so) A common practice is to have `model` name in `camelcase` style</small>


## Create model, controller, migration from single command

```php
php artisan make:model ModelName -mc
```
It will first create model. Then `m` -> `migration`, lastly `c` -> `controller`.

## Update Specific Table

```php
php artisan migrate --path=/database/migrations/2020_04_10_130703_create_test_table.php
```
If you want to rollback specific table

```php
php artisan migrate:rollback  --path=/database/migrations/2020_04_10_130703_create_test_table.php
```

[Ref: Stackoverflow](https://stackoverflow.com/questions/45473624/laravel-migrate-specific-files-from-migrations)

## Write php code

```php
@php
 // your code here
@endphp
 ```
You may also use as you do in raw php like below
```php
<?php
 // your code here
?>
```

## Passing a variable in view 

Ref - [Stackoverflow QA](https://stackoverflow.com/questions/18341792/how-to-pass-data-to-view-in-laravel)

```php
Route::get('/user', function () {
    return view('profile', [
       'variable1' => 'value1' ,
       'variable2'=> 'value2' , // add as much as you want
    ]);
 });
 ```
 To read these variables use in your views
 ```php
 @if($variable1)

 <p> variable1 = {{  $variable1  }}</p>

@endif
```

> Another way using `with()`
```php
return view('index')->with('this_will_be_used_as_variable_in_views',$post);
```
You can also write for passing multiple data from your controller to a view using `with()`
```php
 return \View::make('myHome')
            ->with(compact('project'))
            ->with(['hello'=>$hello])
            ->with(['hello2'=>$hello2])
            ->with(['hello3'=>$hello3]);
```

## Toggle Navbar `active` class

Navbar `active` class using `request()->is('link-name-after-slash')`

```php
<a class="nav-link {{ request()->is('all-post') ? 'active' : '' }}" href="{{ route('admin.allpost') }}">All Posts</a>
```

## How to display html data post in page?
If in your database you have data for display in html form like below,
```
<p>Hello There</p><br><p>How you doing?</p>
```
To show the content use : `{!! content/variable !!}`

Output:
```
Hello There
How you doing?
```

# Query

```php
$count = Blog::select('category')->where('category', $category)->count();
```
Here, `Blog::` model represent `blogs` table which have the following column - id, category, date. Variable `$category = story;` So, we first selected column then defined where to look and then counted.

## Show full blog post/any other data which is in html form. 
(Html form -> data inside of html tags. Like we need to show/print/view `Hello World` which in database/variable like `<h1>Hello World</h1>`)

```php
{!! $blog->post_details !!}
```

## Show html data with limited words
Like if you have a blog post details in data base which is in html form

> Method 1
```php
<p>{{ \Illuminate\Support\Str::words(strip_tags($blog->post_details), 25, '...') }}</p>
```
It will count 25 words. Here First we remove all html tags using php build in method `strip_tags`. Then using `Str::words` we show 25 words and add `...` at the end.
Note. Using Laravel Blade method `{!! !!}` and with `Str::words` we could do also same if data doesn't have html tags. When data have html tags `Str::words` will take 25 words (above example) including html tags first then with `{!! !!}` data will be shown without html tags. But since we took only 25 words we may miss closing brackets and when data shown with `{!! !!}` there will have closing bracket error which may break our frontend design. 

That's why we first remove tags using php method then print limited string.

> Method 2
```php
<p>{{ \Illuminate\Support\Str::limit(strip_tags($blog->post_details), 25, '...') }}</p>
```
It will count 25 characters

> Method 3
```php
<p class="excerpt mb-0">{{ substr(strip_tags($blog->post_details), 0, 25) }}</p>
```
It will count 25 characters

## Share variable across all `controller` and `view`

> Method 1: Using service provider

1. Create a provider. 
```php
php artisan make:provider HelperServiceProvider
```
2. Register this new service provider to `config/app.php`

```php
    'providers' => [

        // ...

        /*
         * Package Service Providers...
         */

        /*
         * Application Service Providers...
         */
        App\Providers\AppServiceProvider::class,
        App\Providers\AuthServiceProvider::class,
        // App\Providers\BroadcastServiceProvider::class,
        App\Providers\EventServiceProvider::class,
        App\Providers\RouteServiceProvider::class,
        App\Providers\HelperServiceProvider::class, // <--- This way
    ],
```


3. Go to `boot` function of our `HelperServiceProvider.php` and add following code

```php
use Illuminate\Support\Facades\View;
use Illuminate\Support\ServiceProvider;

class HelperServiceProvider extends ServiceProvider
{
    // ....

    /**
     * Bootstrap services.
     *
     * @return void
     */
    public function boot()
    {
        $var1 = "This is vari 1";
        $var2 = "This is vari 2";
        View::share(compact('var1', 'var2'));

        // Variable with value
        //View::share('variable_name', 'variable_value');
    }
}
```

4. Now we can use `var1`, `var2` anywhere. Like

```php
Blade : {{ $var1 }}
Controller : $var1
```

**Example**

*HelperServiceProvider.php*
```php
$categorys = ProductCategory::select('category')->get();
View::share(compact('categorys'));
```

*Blade file*
```php
@foreach($categorys as $cat)
    <p>{{ $cat->category }}</p>
@endforeach
```

## Cookie
Goold explanation [Laravel 9 Cookies – Get, Set, Delete Cookie](https://onlinewebtutorblog.com/laravel-9-cookies-get-set-delete-cookie-example/)

## Passing parameters to your controller using anchor tag

Ref: [stackoverflow](https://stackoverflow.com/questions/34810479/how-to-pass-value-inside-href-to-laravel-controller)

`Blade file`
```php
<a href="{!! route('switch', ['prisw'=>$info->prisw, 'secsw'=>$info->secsw]) !!}">Link</a>
```

`web.php`
```php
$router->get('/switchinfo/{prisw}/{secsw}',[
    'uses' => 'SwitchinfoController@switchInfo',
    'as'   => 'switch'
]);
```

`Controller`
```php
<?php namespace App\Http\Controllers;

class SwitchinfoController extends Controller{

    public function switchInfo($prisw, $secsw){
       //do stuffs here with $prisw and $secsw
    }
}
```

## Ajax

```js
$.ajax({
    url: "{{ url("/product-images") }}",
    method: "POST",
    data: {
        _token: '{!! csrf_token() !!}'
    },
    success: function (response){
        console.log(response);
    }
});
```

## Form using ajax

### form
```html
<form id="form_section" action="{{ route('store.category') }}" method="post" enctype="multipart/form-data">
    @csrf

</form>
```


### ajax
```js
$(function (){
    $('#form_section').on('submit', function(e){
        e.preventDefault();
        var form = this;
        $.ajax({
            url:$(form).attr('action'),
            method:$(form).attr('method'),
            data:new FormData(form), _token:'{!! csrf_token() !!}',
            processData:false,
            dataType:'json',
            contentType:false,
            success:function(response){
                console.log(response);
            },
            error: function (xhr){
                console.log(xhr);
            }
        });
    });
});
```

### controller
```php
$request->validate([
    'category' => 'required|string|max:100'
]);

$visibility = $request->visibility ?? "0";

Category::create([
    'category' => $request->category,
    'visibility' => $visibility
]);

return response()->json([
    'message' => 'Success'
]);
```

## Validation

Required: This rule ensures that a given field is present and not empty.
```
'name' => 'required|string'
```
Email: This rule ensures that a given field is a valid email address.
```
'email' => 'required|email'
```
Numeric: This rule ensures that a given field contains only numeric characters.
```
'age' => 'required|numeric'
```
Max: This rule ensures that a given field has a maximum value.
```
'quantity' => 'required|numeric|max:10'
```

Min: This rule ensures that a given field has a minimum value.
```
'price' => 'required|numeric|min:0'
```

Unique: This rule ensures that a given field is unique in the database table.
```
'username' => 'required|unique:users'
```

```
'field_name' => 'unique:table_name,column_name'
```

```PHP
use Illuminate\Support\Facades\DB;
use Illuminate\Validation\Rule;

$validator = Validator::make($request->all(), [
    'email' => [
        'required',
        'email',
        Rule::unique(DB::table('users'), 'email'),
    ],
]);
```


Regex: This rule allows you to define a custom regular expression to validate a given field.
```
'password' => 'required|regex:/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).+$/'
```

Date: This rule ensures that a given field is a valid date.
```
'birthdate' => 'required|date'
```
In: This rule ensures that a given field is one of the specified values.
```
'status' => 'required|in:active,inactive'
```

URL: This rule ensures that a given field is a valid URL.
```
'website' => 'required|url'
```

Image: validation check for image
```
'photo' => 'required|image|mimes:jpeg,png,jpg,gif,svg|max:2048',
```

You can customize the error message for the image rule using the messages method on the Validator instance. For example:
```php
$validatedData = $request->validate([
    'photo' => 'required|image|mimes:jpeg,png,jpg,gif,svg|max:2048',
], [
    'photo.image' => 'The file must be an image.',
    'photo.mimes' => 'The image must be a JPEG, PNG, JPG, GIF, or SVG file.',
    'photo.max' => 'The image may not be greater than 2 megabytes in size.',
]);
```

## Validation message
```php
@if($errors->any())
    @foreach($errors->all() as $error)
    <span class="text-danger">{{ $error }}</span>
    @endforeach
@endif

@if(session('message'))
    <span class="text-info">{{ session('message') }}</span>
@endif

@if(session('success'))
    <span class="text-success">{{ session('success') }}</span>
@endif

@error {{ $message }} @enderror
```

## Redirect Back To specific section

```
use Illuminate\Support\Facades\Redirect;
use Illuminate\Support\Facades\URL;
use Illuminate\Support\Facades\Validator;
```

```
$validator = Validator::make($request->all(), [
            'current_password' => 'required|string',
           'password' => 'required|confirmed|min:8'
        ]);

        if ($validator->fails()) {
            return Redirect::to(URL::previous() . "#password-section")
                ->withErrors($validator);
        }

        $user = User::find(auth()->user()->id);


        if(!Hash::check($request->current_password, $user->password)){
            return Redirect::to(URL::previous() . "#password-section")->with('error', 'Current passowrd is not match!!');
        }else{
            User::where('id', auth()->user()->id)->update(['password'=>Hash::make($request->password)]);
        }

        return Redirect::to(URL::previous() . "#password-section")->with('success', 'Password updated successfully!');

```

## Faker

[Main Github Repo](https://github.com/fzaninotto/Faker)

[losing-session-data-after-post-from-third-party-website-like-payment-gateway](https://stackoverflow.com/questions/67692358/losing-session-data-after-post-from-third-party-website)
