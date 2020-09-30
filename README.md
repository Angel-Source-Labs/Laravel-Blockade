# Laravel Blockade

[![Latest Stable Version](https://img.shields.io/packagist/v/romanzipp/Laravel-Blockade.svg?style=flat-square)](https://packagist.org/packages/romanzipp/laravel-blockade)
[![Total Downloads](https://img.shields.io/packagist/dt/romanzipp/Laravel-Blockade.svg?style=flat-square)](https://packagist.org/packages/romanzipp/laravel-blockade)
[![License](https://img.shields.io/packagist/l/romanzipp/Laravel-Blockade.svg?style=flat-square)](https://packagist.org/packages/romanzipp/laravel-blockade)
[![GitHub Build Status](https://img.shields.io/github/workflow/status/romanzipp/Laravel-Blockade/Tests?style=flat-square)](https://github.com/romanzipp/Laravel-Blockade/actions)

A simple but highly customizable package for preventing access to WIP Laravel projects.

## Installation

```
composer require romanzipp/laravel-blockade
```

**If you use Laravel 5.5+ you are already done, otherwise continue.**

Add Service Provider to your `app.php` configuration file:

```php
romanzipp\Blockade\Providers\BlockadeServiceProvider::class,
```

## Configuration

Copy configuration to config folder:

```
$ php artisan vendor:publish --provider="romanzipp\Blockade\Providers\BlockadeServiceProvider"
```

### Handlers

Handlers are responsible validating authentication requests and sending successful or failed responses. You can customize each handler via the `blockade.handlers.*` config entries.

| Handler | Description | Class |
| --- | --- | --- |
| **Form** (default) | The password is provided by a form | [romanzipp\Blockade\Handlers\FormHandler](https://github.com/romanzipp/Laravel-Blockade/blob/master/src/Handlers/FormHandler.php) |
| Query Parameter | The password is attached as query parameter | [romanzipp\Blockade\Handlers\QueryParameterHandler](https://github.com/romanzipp/Laravel-Blockade/blob/master/src/Handlers/QueryParameterHandler.php) | 

### Stores

Stores are storing (how surprising) the authentication state for later requests. You can customize each handler via the `blockade.stores.*` config entries.

| Store | Description | Class |
| --- | --- | --- |
| **Cookies** (default) | The password hash will be stored as browser cookie | [romanzipp\Blockade\Stores\CookieStore](https://github.com/romanzipp/Laravel-Blockade/blob/master/src/Stores/CookieStore.php) |
| Session | The password hash will be stored in the active session | [romanzipp\Blockade\Stores\SessionStore](https://github.com/romanzipp/Laravel-Blockade/blob/master/src/Stores/SessionStore.php) | 

## Usage

Add the Blockade middleware to your HTTP kernel:

```php
namespace App\Http;

use Illuminate\Foundation\Http\Kernel as HttpKernel;
use romanzipp\Blockade\Http\Middleware\BlockadeMiddleware;

class Kernel extends HttpKernel
{
    protected $middleware = [
        // ...
        BlockadeMiddleware::class,
        // ...
    ];
}
```

## Testing

```
./vendor/bin/phpunit
```
