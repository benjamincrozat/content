---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/benjamincrozat/content/assets/3613731/6b486727-4fca-4624-8e61-b01f2c526d76
Title: How to customize default middleware in Laravel 11
Description: The new minimalist application skeleton in Laravel 11 comes without middleware classes. Here's how to customize them.
Canonical:
Audio:
Published at: 2024-02-25
Modified at:
Categories: laravel
---

## Introduction to default middleware customization in Laravel 11

Starting from [Laravel 11](https://laravel.com/docs/11.x/releases), new projects get to experience a slimmer skeleton. Parts of the efforts to make it happen was to remove the default middleware classes.

But how do you customize them then? Easy! Just go into your *bootstrap/app.php* file and configure them however you want. Let me show you in more details for the most common use cases.

## Customize where guests are redirected

To customize where guests are redirected, use the `redirectGuestsTo()` method in _bootstrap/app.php_:

```php
->withMiddleware(function (Middleware $middleware) {
    $middleware->redirectGuestsTo('/admin/login');
})
```

Previously, this was happening in the *Authenticated.php* middleware class.

## Customize where users and guests are redirected (previously in *Authenticated.php* and *RedirectIfAuthenticated.php*)

To customize where users and guests are redirected, use the `redirectTo()` method in _bootstrap/app.php_:

```php
->withMiddleware(function (Middleware $middleware) {
    $middleware->redirectTo(
        guests: '/admin/login',
        users: '/dashboard'
    );
})
```

Previously, this was happening in the *Authenticated.php* and *RedirectIfAuthenticated.php* middleware classes.