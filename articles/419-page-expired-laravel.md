---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/40/Data_security_24_bxnctl.png
Title: Here's how to fix the "419 Page Expired" error in Laravel
Description: Here's how to fix one of the most frequent issues in Laravel and learn exactly why it happens.
Canonical: 
Published at: 2023-06-26
Modified at: 2023-08-12
Categories: laravel, security
---

## Introduction

Have you ever encountered the "Page Expired" error with the HTTP code 419 in your Laravel applications?

It's often a simple issue related to CSRF (Cross-Site Request Forgery) tokens.

Let's see what it means and how to fix it.

##  Why "419 Page Expired" happens and how to fix it

In your Laravel 8, 9 or 10 applications, whatever the version you are running is, you have likely used the `@csrf` directive in your forms.

This directive generates a hidden input field containing a CSRF token automatically included when submitting the form.

This token confirms that the form is being submitted from your application and not by a third party.

Errors like the "419 Page Expired" occur when the CSRF token is mismatched. This can happen for various reasons:

- Sometimes, you just let the page open for too long and the token expired, which is a good thing. Just click the refresh button in your browser and re-send the form.
- Or it might just be because you forgot to include the `@csrf` directive inside your form. This is problematic, because by default, Laravel expects the CSRF token to be present thanks to the `VerifyCsrfToken` middleware that filters the requests.

Learn more on Laravel's documentation about [Cross-Site Request Forgery protection](https://laravel.com/docs/10.x/csrf).

## Disable CSRF protection on some pages

Occasionally, you may want to disable CSRF protection on some pages and definitely kill those 419 HTTP codes.

Instead of removing the middleware from the kernel, you could just specify which pages you want to exclude from being protected.

In *app/Http/Middleware/VerifyCsrfToken.php*:

```php
namespace App\Http\Middleware;

use Illuminate\Foundation\Http\Middleware\VerifyCsrfToken as Middleware;

class VerifyCsrfToken extends Middleware
{
    /**
     * The URIs that should be excluded from CSRF verification.
     *
     * @var array<int, string>
     */
    protected $except = [
        '/some-page',
        '/some-other-page',
    ];
}
```

