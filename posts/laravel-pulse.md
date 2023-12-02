---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/256/01HFEMVGDB82X8N51ZE7EYA0MG.jpg
Title: Laravel Pulse: monitor your apps for free
Description: Discover Laravel Pulse, a free, open-source package offering real-time app monitoring, usage statistics, queue monitoring, and more.
Canonical: 
Audio:
Published at: 2023-11-17
Modified at: 2023-12-01
Categories: laravel, packages
---

## What Laravel Pulse is

**[Laravel Pulse](https://pulse.laravel.com) is a free and open source package for the [Laravel framework](https://laravel.com) that helps developers monitor various aspects of their web applications in real-time.**

Taylor Otwell, the creator of Laravel, [said](https://twitter.com/taylorotwell/status/1725210034399797365) that the tool was born out of frustration he had with Laravel Forge and its inability to quickly diagnose why the service was underperforming and which users were causing that.

I still can't believe such a tool can be free, but there we are!

![Laravel Pulse's dashboard in action.](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/255/conversions/01HFEMTCB9RCHDFGV1EZYRGVV5-medium.jpg)

## Laravel Pulse release date

According to Taylor Otwell, the team still needs to refine the package before releasing the first beta version. It should be in your hands between November 27 and December 1, 2023. Of course, unforeseen events can happen, so don't expect this timeframe to be accurate.

https://twitter.com/taylorotwell/status/1727862264982577256

## The features Laravel Pulse offers

- **Application usage of your users**: Laravel Pulse lets you see which of your users consume the most resources. It uncovers which ones make the most requests, engage with the slowest endpoints, and dispatch the most jobs throughout your application.
- **Statistics of your servers**: Monitor various aspects of your servers, like CPU, memory, and disk usage. All of this in one place!
- **Queue monitoring**: Instead of trying to guess which queue needs more resources, make educated decisions based on historical data and bring real benefits to your users. 👌
- **Performance monitoring**: Again, making decisions based on data is invaluable, and Laravel Pulse can also help with routes, database queries, jobs, and even outgoing requests.
- **Trending exceptions**: It's like having a highly lightweight error-tracking tool. You will see which exceptions are the most frequent and how they could be related to your performance issues.
- **Custom community-powered metrics**: Laravel Pulse will undoubtedly be customizable, and I'll share whatever I can find from the community here on my blog.
- **Custom dashboard layout**: It's mentionned on the official website that the dashboard's layout can be customized, which is great news!

## Install Laravel Pulse

**For now, Laravel Pulse requires a MySQL database. If you are running something else, that's fine, but you will have to create a new database connection for MySQL.**

**Pulse is still in beta** and you have to make some changes to your *composer.json* file to install it until a stable version is released. Change the `minimum-stability` to `beta` and make sure `prefer-stable` is set to `true`:

```json
"minimum-stability": "beta",
"prefer-stable": true
```

Then, just to install Pulse, use the following command:

```bash
composer require laravel/pulse
```

## Set up Laravel Pulse

To set up Laravel Pulse, you will need to ensure it has a database in which it can store the data it collects. You can do this by running the migrations (which you don't need to publish):

```bash
php artisan migrate
```

Once this is done, open your browser and hit the route `/pulse`. It was that simple.

![Laravel Pulse right after it has been installed.](https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/benjamincrozat/content/assets/3613731/16b61b08-db6d-47ee-8439-ae8c34ba371f)

## Monitor your server

Right now, our new installation of Pulse is empty.

We have to display information in there and I suggest we start with your server's resources.

To do this, run the following command:

```bash
php artisan pulse:check
```

This command runs continuously to provide Pulse with the needed data. This is a daemon you have to run in the background, and I recommend you to use [Supervisor](http://supervisord.org) to do so.

![Laravel Pulse's php artisan pulse:check command in action.](https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/benjamincrozat/content/assets/3613731/cad320da-6181-4961-9bd1-11a7249efa26)

## Contribute to Laravel Pulse

Laravel Pulse's is free, open source, and is available through a GitHub repository at [laravel/pulse](https://github.com/laravel/pulse). You can send as many Pull Requests as you want for bug fixes and enhancements.
