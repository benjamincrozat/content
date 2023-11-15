---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/222/Oezl6om6sBJmaiKSF2sh78yXpzyNvp-metacGhwLTkwLnBuZw%3D%3D-.png
Title: An early look at PHP 9.0's new features and changes
Description: PHP 9.0 is still far in the future. We don't know a lot, but we have a few breaking changes planned for it.
Canonical: 
Audio:
Published at: 2023-11-03
Modified at: 
Categories: php
---

## Introduction

PHP is an open-source project. Knowing what's going on for the next version only takes a minute of research. For instance, this page lists all the [accepted RFCs for different versions of PHP](https://wiki.php.net/rfc).

That being said, despite PHP 9.0 being planned, no work have been started yet and we have to dig deeper.

## When will PHP 9.0 be released?

**For now, the release date of PHP 9.0 hasn't been announced yet.** This version is still far in the future. We could get PHP 8.5 and 8.6 before 9.0 is even considered. Who knows?

## How to install and test PHP 9.0?

To this day, no work has been started on PHP 9.0, so you won't even be able to pull the latest code and compile it yourself.

## What's new in PHP 9.0

### Deprecated features from earlier PHP versions will be removed

**Features that have been deprecated in PHP 8.1, 8.2, 8.3, and 8.4 ([learn more about PHP 8.4](/php-84)) will finally removed in PHP 9.0.** This will translate to breaking changes for developers who ignored the warnings. 😅

Here's a list of RFCs containing all the deprecated features:
- [PHP RFC: Deprecations for PHP 8.1](https://wiki.php.net/rfc/deprecations_php_8_1)
- [PHP RFC: Deprecations for PHP 8.2](https://wiki.php.net/rfc/deprecations_php_8_2)
- [PHP RFC: Deprecations for PHP 8.3](https://wiki.php.net/rfc/deprecations_php_8_3)
- [PHP RFC: Deprecations for PHP 8.4](https://wiki.php.net/rfc/deprecations_php_8_4)

### Some warnings will become errors in PHP 9.0

In order to make PHP more reliable, warnings for undefined variables and properties will now become errors.

For instance, the following code will not run anymore in PHP 9.0:

```php
// PHP 8.x: "Warning: Undefined variable $foo"
// PHP 9.0: "Fatal error: Uncaught Error: Undefined variable '$foo'"
echo $foo;
```

Also, from what I understand, these changes with variables and properties will make the maintainers' lives easier, which is good for everyone!

I let you check out the RFCs for more details:
- [PHP RFC: Undefined Variable Error Promotion](https://wiki.php.net/rfc/undefined_variable_error_promotion)
- [PHP RFC: Undefined Property Error Promotion](https://wiki.php.net/rfc/undefined_property_error_promotion)