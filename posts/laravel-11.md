---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/26/laravel-11_zv4zly.png
Title: Laravel 11: release date and new features
Description: Laravel 11 will be released on February 6th, 2024. Its development is still ongoing. Let's dive into every relevant new feature we know about already.
Canonical: 
Audio:
Published at: 2023-01-05
Modified at: 2023-09-17
Categories: laravel
---

## When will Laravel 11 be released?

According to the [Support Policy](https://laravel.com/docs/10.x/releases#support-policy), **Laravel 11 is scheduled to be released on February 6th, 2024**.

The release of Laravel 11 doesn't mean you must update all your projects immediately, though.

The framework last had LTS (Long-Term Support) in version 6, but **each major version has two years of updates**, which should give you enough time to get your codebase in check and upgrade it.

Laravel 10 will receive bug fixes until August 6th, 2024 and security fixes until February 4th, 2025.

| Version | PHP | Release | Bug fixes until | Security fixes until |
| ------- | --- | ------- | --------------- | -------------------- |
| 10 | 8.1 | February 14, 2023 | August 6th, 2024 | February 4th, 2025 |
| 11 | 8.2 | Q1 2024 | August 5th, 2025 | February 3rd, 2026 |

## How to install Laravel 11?

Laravel 11 hasn't been released. Therefore, you must use the `--dev` flag on the official Laravel installer, which pulls the *main* branch from the [laravel/laravel](https://github.com/laravel/laravel) repository that always contains the latest code.

```bash
laravel new hello-world --dev
```

Or, if you prefer to use Composer explicitly:

```bash
composer create-project --prefer-dist laravel/laravel hello-world dev-master
```

## What's new in Laravel 11: features and changes

### Laravel 11 drops support for PHP 8.1

When Laravel 11 is released, PHP 8.2 will be established, and PHP 8.3 will also be stable. With support for the last two major versions of PHP, Laravel can move forward and abandon 8.1.

But remember: your Laravel apps don't need to be updated to the latest and greatest as soon as they're released.

Especially if you have projects with paid clients or employees who depend on them to do their work.

Those projects need to slowly but surely move forward by doing extensive testing. Don't rush.

See the pull request on GitHub: [[11.x] Drop PHP 8.1 support](https://github.com/laravel/framework/pull/45526)

![PHP 8.2](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/127/conversions/www.php.net_releases_8.2_en.php_jqtup2-medium.jpg)

### Laravel 11 introduces a more minimalistic application skeleton

Laravel 11 comes with a slimmer application skeleton. The idea for this is that you should have less boilerplate code to deal with. I couldn't agree more. Here are the details of this change:

- In `AuthServiceProvider`, the `$policies` property has been removed, as the framework automatically discovers them.

- In `EventServiceProvider`, the `SendEmailVerificationNotification` is no longer necessary, as the base `EventServiceProvider` is registering it. You will also notice that auto-event discovery is now enabled by default. 

- `BroadcastServiceProvider` no longer necessary and has been removed. The framework is not automatically loading the *routes/channels.php* file.

- `RedirectIfAuthenticated` is now simpler thanks to the base one in the framework's internals.

- The `Authenticate` middleware no longer calls `redirectTo()` for JSON routes. This removes an unnecessary ternary check.

- `EncryptCookies`, `PreventRequestsDuringMaintenance.php`, `TrimStrings`, `TrustHosts`, `TrustProxies`, `ValidateCsrfToken` and `ValidateSignature` middlewares have been removed from the skeleton.

- Custom Artisan commands are now loaded automatically. The console kernel does not need to call the `load()` method.

- The *routes/console.php* has been removed. Closure-based Artisan commands can be registered in the console kernel.

- Some migrations have been consolidated into a single file or just removed.

- The `AuthorizesRequests` and `ValidatesRequests` traits have been removed from the base controller.

- The *bootstrap/app.php* file has been shrunk to just three lines of code.

- The exception handler was removed.

Here's the original PR for Laravel 10 ([[10.x] Slimmer Application Skeleton](https://github.com/laravel/laravel/pull/6172)), which was later moved to Laravel 11. You will find even more information about what was changed.

### New feature: Laravel 11 offers a new Dumpable trait (dump() and dd() from your objects)

This pull request introduces a new `Dumpable` trait in Laravel 11, intended to replace the current `dd` and `dump` methods in most of the framework's classes.

The trait allows Laravel users and package authors to include debugging methods easily within their classes by utilizing this trait.

Here's a code example showing how it can be used:

```php
<?php

namespace App\ValueObjects;

use Illuminate\Support\Traits\Dumpable;
use Illuminate\Support\Traits\Conditionable;

class Address
{
    use Conditionable, Dumpable;

    // ...
}

$address = new Address;

// Before: 
$address->foo()->bar();

// After:
$address->foo()->dd()->bar();
```

See the pull request on GitHub: [[11.x] Adds Dumpable concern](https://github.com/laravel/framework/pull/47122)


### New feature: The new and more convenient Model::casts() method goes live Laravel 11

Usually, in Laravel, you declare attribute casting in an Eloquent model like this:

```php
class User extends Model
{
    protected $casts = [
        'email_verified_at' => 'datetime',
    ];
}
```

With Laravel 11, you can now define your casting through a `casts()` method in your model, giving you a chance to use static methods from the class doing the casting. This is how it looks:

```php
class User extends Model
{
    protected function casts(): array
    {
        return [
            'foo' => AsCollection::using(FooCollection::class),
        ];
    }
}
```

Moreover, you can now also specify your casts as an array:

```php
class User extends Model
{
	// Even in the old $casts property!
    protected $casts = [
        'foo' => [AsCollection::class, FooCollection::class],
    ];
  
    protected function casts() : array
    {
        return [
            'foo' => [AsCollection::class, FooCollection::class],
        ];
    }
}
```

The `casts()` method is prioritized over the `$casts` property.

All these changes are non-breaking, meaning they won't affect your current code if you update to Laravel 11.

See the pull request on GitHub: [[11.x] Adds Model::casts() method and named static methods for built-in casters](https://github.com/laravel/framework/pull/47237)

### Laravel 11 release preparation pull requests

Here's a list of every merged PR I found to prepare the release of Laravel 11:

- [[11.x] Set up Laravel v11](https://github.com/laravel/framework/pull/45525)
- [[11.x] Update Testbench dependencies for Laravel 11](https://github.com/laravel/framework/pull/45538)
- [[11.x] Removed old WithoutEvents trait](https://github.com/laravel/framework/pull/47180)
- [And more!](https://github.com/laravel/framework/pulls?q=is%3Apr+is%3Amerged+%5B11.x%5D+)

There are a lot of small details to dig into that I didn't include in this article for the sake of conciseness.

## How to contribute your own features and bug fixes to Laravel 11?

Did you know you can fix the bugs you have encountered or create the next big feature for Laravel 11?

1. See what's going on for Laravel 11 on GitHub: https://github.com/laravel/framework/pulls. The Pull Requests will tell you what's already been done.
2. Take one of your pain points with the framework and create a solution yourself.
3. Send the PR over to the laravel/framework repository, collect feedback, improve, and get merged.

One important tip to increase your chances of being merged: add something to the framework that's a win for developers but not a pain to maintain for Taylor and his team in the long run.

![Pull requests on the laravel/framework repository.](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/128/conversions/Screenshot_2023-01-05_at_18.03.30_qx8sjy-medium.jpg)

---

**This is what's new in Laravel 11 for now.**

**There's more to come until February 2024, though, so stay tuned!**

