---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/benjamincrozat/content/assets/3613731/25257e56-cefe-4a4a-b3ba-48b6709829fe
Title: How to publish config files in Laravel 11 and up
Description: The new minimalist application skeleton in Laravel 11 comes with no configuration files. Here's how to publish them.
Canonical:
Audio:
Published at: 2024-02-23
Modified at:
Categories: laravel
---

Starting from Laravel 11, new projects get to experience a slimmer skeleton. Parts of the efforts to make it happen was to remove the configuration files which can be overwhelming for new developers.

That being said, as your application grows, you might need to tweak some configuration values. So to publish your config files in Laravel 11 and up, use:

```bash
php artisan config:install
```

Laravel will then ask you to choose which config file you want to publish so you don't bloat up your application.

That being said, you can also publish them all using:

```bash
php artisan config:install --all
```
