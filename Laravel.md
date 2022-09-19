<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

# Laravel Common Commands

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

## Adding CSS / JS links

If you want use css/js files from local, place files in public folder. Then,

```css
<link rel="stylesheet" href="{{ asset('css/bootstrap.min.css') }}">
```
<small>Here `bootstrap.min.css` file is in css folder. That `css` folder inside of `public` folder.</small>

## Create model, controller, migration

> Migration
```php
php artisan make:migration migration_names
```
<small>Note: (Not necessary to follow. Just many dev do so) A common practice is to have `migration` name in `plural` form</small>

> Controller
```php
php artisan make:controller NameController
```
<small>Note: (Not necessary to follow. Just many dev do so) A common practice is to have `controller` name in `camelcase` style and end with `controller` word</small>

> Model
```php
php artisan make:model ModelName
```
<small>Note: (Not necessary to follow. Just many dev do so) A common practice is to have `model` name in `camelcase` style</small>


## Create model, controller, migration from single command

```php
php artisan make:model ModelName -mc
```
It will first create model. Then `m` -> `migration`, lastly `c` -> `controller`.

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

## Passing a variable in view. Ref - [Stackoverflow QA](https://stackoverflow.com/questions/18341792/how-to-pass-data-to-view-in-laravel)

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