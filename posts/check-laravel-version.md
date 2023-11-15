---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/3/programmer_v_02_pbqu54.jpg
Title: 6 ways to check which Laravel version you are running
Description: Knowing which Laravel version you are running is important before you start writing code on a new project. There are multiple ways to do so.
Canonical: 
Audio:
Published at: 2022-09-10
Modified at: 2023-10-09
Categories: laravel
---

## Introduction

**The quickest way to check your Laravel version is by using the `php artisan --version` command.**

Knowing which version of Laravel you are running and its [specific details](/laravel-versions) are crucial pieces of information, whether you're planning to upgrade, debug, or simply want to ensure compatibility with a specific feature.

However, there are other methods to get the version of Laravel. Here's a comprehensive guide with commands that work no matter if you use macOS, any Linux distribution like Ubuntu, Docker or WSL (Windows Subsystem for Linux).

## How to check the version of Laravel

### Using the `php artisan about` command

The about command Artisan offers not only displays the Laravel version but also other helpful information about your project such as the version of PHP you're running on, Composer's version, cache drivers, etc.

However, it's important to note that the about command is only available in Laravel version 8 or later.

```
php artisan about
  
Laravel Version ..................................................... 9.43.0  
PHP Version ......................................................... 8.1.10  
Composer Version ..................................................... 2.4.1
```

![The php artisan about command in Laravel.](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/73/conversions/CleanShot_2023-04-21_at_12.03.38_2x_ydqmbj-medium.jpg)

### Using the --version flag with Artisan

I talked about it in the introduction. If you are using an older version of Laravel, you can still use the `--version` flag to display the Laravel version.

This is the original method for checking it before the about command was introduced. The `--version` flag has priority over any Artisan command.

```
php artisan --version

Laravel Framework 9.43.0
```

Or, using the flag with any other command:

```
php artisan make:model --version

Laravel Framework 9.43.0
```

### Using the version() method

The [`app()`](https://laravel.com/docs/helpers#method-app) helper will give you access to many information, such as the Laravel version you are running. Try this simple code below:

```php
// 9.43.0
app()->version();
```

You could use it in a custom dashboard you created:

```blade
<ul>
    <li>PHP: {{ phpversion() }}</li>
    <li>Laravel: {{ app()->version() }}</li>
</ul>
```

### Via Composer in your terminal

Composer offers a handy command to check the version of a specific dependency. Run:

```bash
composer show laravel/framework
```

You will get an incredibly report about this dependency.

```
name     : laravel/framework
descrip. : The Laravel Framework.
keywords : framework, laravel
versions : * v10.26.2
type     : library
license  : MIT License (MIT) (OSI approved) https://spdx.org/licenses/MIT.html#licenseText
homepage : https://laravel.com
source   : [git] https://github.com/laravel/framework.git 6e5440f7c518f26b4495e5d7e4796ec239e26df9
dist     : [zip] https://api.github.com/repos/laravel/framework/zipball/6e5440f7c518f26b4495e5d7e4796ec239e26df9 6e5440f7c518f26b4495e5d7e4796ec239e26df9
path     : /Users/benjamin/Projects/benjamincrozat/vendor/laravel/framework
names    : laravel/framework, psr/container-implementation, psr/simple-cache-implementation, illuminate/auth, illuminate/broadcasting, …
…
```

![The command `composer show` in action to check the version of Laravel.](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/191/conversions/hLcwhyE2sPfLN94vR633i9MKlI8865-metaQ2xlYW5TaG90IDIwMjMtMTAtMDkgYXQgMTYuNDAuMzBAMngucG5n--medium.jpg)

### In the composer.json and composer.lock files

In your *composer.json*, you will be able to get the minimum version of Laravel your project is locked on:

```json
"require": {
    "php": "^8.0.2",
    "guzzlehttp/guzzle": "^7.2",
    "laravel/framework": "^9.19",
    "laravel/sanctum": "^3.0",
    "laravel/tinker": "^2.7"
}
```

As you can see, this project is locked on Laravel 9.19 or earlier.

But this might not be enough. Since versions earlier than 9.19 are supported, you project might use Laravel 9.32 or even 9.484843!

Instead, search for "laravel/framework" inside your *composer.lock* file to get the exact Laravel version that's installed on your project :

```json
{
    "name": "laravel/framework",
    "version": "v9.43.0",
    "source": {
        "type": "git",
        "url": "https://github.com/laravel/framework.git",
        "reference": "2ca2b168a3e995a8ec6ea2805906379095d20080"
    }
}
```

### In the source code

Open your favorite code editor and search for *vendor/laravel/framework/src/Illuminate/Foundation/Application.php*. The exact version of Laravel you are using is written in the `VERSION` constant.

```php
class Application extends Container implements ApplicationContract, CachesConfiguration, CachesRoutes, HttpKernelInterface
{
    const VERSION = '9.43.0';
}
```

This is actually the constant `app()->version()` uses. 😀

```php
public function version()
{
    return static::VERSION;
}
```

