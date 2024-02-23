---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/benjamincrozat/content/assets/3613731/67c22860-75a2-43a0-960a-60c4f839c287
Title: How to publish the lang directory in Laravel 11 and up
Description: The new minimalist application skeleton in Laravel 11 comes with no lang directory. Here's how to publish it.
Canonical:
Audio:
Published at: 2024-02-23
Modified at:
Categories: laravel
---

Starting from Laravel 11, new projects get to experience a slimmer skeleton. Parts of the efforts to make it happen was to remove the _lang_ directory so new developers don't feel overwhelmed.

That being said, as your application grows, you might need to add new languages. Therefore, to publish the _lang_ directory in Laravel 11 and up, use:

```bash
php artisan lang:publish
```

And if you already have a _lang_ directory and want to overwrite what's already been published, use:

```bash
php artisan lang:publish --existing
```
