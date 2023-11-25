---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/40/Data_security_24_bxnctl.png
Title: Here's how to fix the "419 Page Expired" error in Laravel
Description: Here's how to fix one of the most frequent issues in Laravel and learn exactly why it happens.
Canonical: 
Audio:
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

- Sometimes, you just let the page open for too long and the token expires, which is a good thing. Just click the refresh button in your browser and re-send the form.
- Or it might be because you forgot to include the `@csrf` directive in your form. This is problematic because, by default, Laravel expects the CSRF token to be present thanks to the `VerifyCsrfToken` middleware that filters the requests.

Learn more on Laravel's documentation about [Cross-Site Request Forgery protection](https://laravel.com/docs/10.x/csrf).

## Disable CSRF protection on some pages

Occasionally, you may want to disable CSRF protection on some pages and kill those 419 HTTP codes.

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
## Issues Particular to Logout
Best practice for user logout is that the logout button should create a post request, and that post should be protected by csrf.  
The reason for this is because in some scenarios it can assist an attacker to see you login, but to do that they must first log you out. 
Protecting the logout form from CSRF attacks blocks this scenario.

However, the csrf token on the logout form can become stale in at least three scenarios.

1. User has multiple tabs open and logs out in one of them. Other tabs look fine but the logout no longer works
2. The user leaves their desk for more than the session timeout. They return to their computer later and press logout.
3. The user chooses the option to logout other devices when logging in on a new device.

In each case, the user pressing the logout button will be presented with a 419 error and not know if they had logged out or not.

The solution is a simple change to the handle method in the VerifyCsrfToken middleware.

In *app/Http/Middleware/VerifyCsrfToken.php*:

```php
    public function handle($request, Closure $next)
    {
        if($request->route()->named('logout')) {

            if (!Auth::check() || Auth::guard()->viaRemember()) {

                $this->except[] = route('logout');
                
            }   

        }

        return parent::handle($request, $next);
    }
```
The modification applies the logic;

If the route is logout, and the user is not logged in, and they have not just been logged in via the remember me function.

Then, dynamically add logout to the array of csrf exceptions.

So, for all other forms, apply csrf as normal, but for the logout form, if the user is already without a session (and therefore not logged in) then csrf should be ignored.

The logout function will process as normal, and the user sees no issue.

