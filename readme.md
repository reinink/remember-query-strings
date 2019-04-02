# Remember Query Strings

Remember Query Strings is a Laravel middleware that automatically remembers and restores query strings. It does this by remembering the last query strings visited in the session. Later, when you visit that same route, if no query strings are provided, the middleware will automatically restore them from the sessions via a redirect.

## Installation

You can install this package via Composer:

```
composer require reinink/remember-query-strings
```

## Setup

First register the route middleware in your `App\HttpKernel` class:

```php
protected $routeMiddleware = [
    // ..
    'remember' => \Reinink\RememberQueryStrings::class,
];
```

## Usage

Now you can use this middleware just like [any other middleware](https://laravel.com/docs/middleware). For example, in your routes:

```php
Route::get('users')->name('users')->uses('UsersController@index')->middleware('remember');
```

Or in a controller:

```php
class UserController extends Controller
{
    public function __construct()
    {
        $this->middleware('remember')->only('index');
    }
}
```

## Opting out

If you'd like to visit a page without remembering the query strings, pass `?remember=no` to disable this behviour for that visit.

## Forgetting query strings

To forget previously remembered query strings, simply pass `?remember=forget`.
