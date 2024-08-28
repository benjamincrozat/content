---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/user-attachments/assets/2e4c7701-a2c5-4cdd-aa1c-9326ac56bad3
Title: What's new in Pest 3 and how to upgrade
Description: Step up your PHP testing game with Pest 3. Architecture tests presets, mutations, and todo lists management.
Canonical: 
Audio:
Published at: 2024-08-27
Modified at:
Categories: php
---

## Introduction

[Pest](https://pestphp.com), my favorite PHP testing framework, has just dropped its version 3, and I couldn't wait to dive in and share my thoughts with you.

## The easiest upgrade ever?

Before we get into the juicy new features, let's talk about upgrading. Spoiler alert: it's ridiculously simple. All you need to do is bump up your dependency to `^3.x-dev` and change `minimum-stability` to `dev` in your `composer.json` file. That's it! No breaking changes to worry about, no tedious refactoring – just a smooth sail to the latest and greatest version of Pest.

```json
{
    "require-dev": {
        "pestphp/pest": "^3.x-dev"
    }
}
```

Run `composer update`, and you're good to go. Now, let's dive into what's new!

## What's new in Pest 3?

### Architecture tests presets

One of the standout features in Pest 3 is the introduction of architecture tests presets. This is a powerful tool that allows us to enforce architectural rules and best practices in our codebase. And the best thing being that we don't have to write them ourselves!

Pest 3 comes with several presets out of the box:

- Laravel
- PHP
- Relaxed
- Security
- Strict

Using these presets is as simple as calling a method. For example, if you're working on a Laravel project, you can use the Laravel preset like this:

```php
arch()->preset()->laravel();
```

This will apply a set of architectural rules that are tailored for Laravel applications, helping you maintain a clean and consistent codebase.

But what if you need to make exceptions? Pest 3 has got you covered. You can exclude specific files or namespaces using the `ignoring()` method. For instance:

```php
arch()->preset()->laravel()->excluding('App\Models\Scopes');
```

This flexibility allows you to adhere to best practices while still accommodating the unique needs of your project.

### Mutation testing: how reliable are your tests?

Pest 3 is bringing mutation testing to the table! This feature enhances the reliability of your test suites by making small changes to your code and running tests against these mutated versions.

To get started with mutation testing, install the plugin:

```bash
composer require pestphp/pest-plugin-mutate --dev
```

Once installed, you can run mutation tests with this simple command:

```bash
./vendor/bin/pest --mutate
```

I ran this on my project, and here's what it looks like:

![Pest's mutation tests in action.](https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/user-attachments/assets/fe303b15-3a35-4f8b-8a6b-f066e566576c)

As you can see, this is a disaster. But for my defense, it's a new project and a work in progress!

For more information and detailed documentation, check out the [Pest Mutate Plugin GitHub repository](https://github.com/pestphp/pest-plugin-mutate).

### Todos management with GitHub

Another intriguing feature coming with Pest 3 is todos management integrated with GitHub.

While the specifics aren't clear yet, this sounds like it could be a great way to keep track of tasks and improvements directly from your test suite. Imagine being able to flag areas that need attention and have them automatically sync with your GitHub issues – that's the kind of seamless workflow I'm always excited about.

I'll be sure to update you all once I have more information on how this feature works and how we can leverage it in our projects.
