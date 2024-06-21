---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/40/Data_security_24_bxnctl.png
Title: Here's how to fix the "419 Page Expired" error in Laravel
Description: Here's how to fix the "419 Page Expired" error in Laravel and learn exactly why it happens.
Canonical: 
Summary: https://nobinge.ai/conversations/4e06a436-39e2-4e1c-9b68-fd4df93801e9
Audio: https://cdn.benjamincrozat.com/419-page-expired-laravel.mp3
Published at: 2023-06-26
Modified at: 2024-06-21
Categories: laravel, security
---

## Introduction to the "419 Page Expired" error in Laravel

Have you ever encountered the "Page Expired" error with the HTTP code 419 in your Laravel applications?

It's often a simple issue related to CSRF (Cross-Site Request Forgery) tokens.

Let's see what it means and how to fix it.

##  Why "419 Page Expired" happens and how to fix it

In your Laravel 8, 9, or 10 applications, whatever the version you are running is, you have likely used the `@csrf` directive in your forms.

This directive generates a hidden input field containing a CSRF token, which is included when submitting the form.

This token confirms that the form is being submitted from your application and not by a third party.

Errors like the "419 Page Expired" occur when the CSRF token is mismatched. This can happen for various reasons:

- Sometimes, you let the page open for too long (a login page for instance), and the token expires, which is good. Just click the refresh button in your browser and re-send the form.
- Or it might be because you forgot to include the `@csrf` directive in your form. This is problematic because, by default, Laravel expects the CSRF token to be present thanks to the `VerifyCsrfToken` middleware that filters the requests.

Learn more on Laravel's documentation about [Cross-Site Request Forgery protection](https://laravel.com/docs/10.x/csrf).

## Disable CSRF protection on some pages to avoid the "419 Page Expired" error

Occasionally, you may want to disable CSRF protection on some pages and kill those "419 Page Expired" errors.

Instead of removing the middleware from the kernel, specify which pages you want to exclude from being protected.

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
