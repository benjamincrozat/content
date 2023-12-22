---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/58/php-84_kkilmr.jpg
Title: PHP 8.4: new features and release date
Description: PHP 8.4 is expected to drop on November 21, 2024. Let's review the known new features and changes.
Canonical: 
Audio:
Published at: 2023-09-01
Modified at: 2023-12-22
Categories: php
---

## Introduction

PHP is an open-source project. Knowing what's going on for PHP 8.4 only takes a minute of research. For instance, this page lists all the [accepted RFCs for different versions of PHP](https://wiki.php.net/rfc#php_84), including PHP 8.4.

## When will PHP 8.4 be released?

PHP 8.4 will be released on November 21, 2024, according to the [preparation tasks list](https://wiki.php.net/todo/php84). It will be tested through three alpha releases, three betas, and six release candidates.

| Date               | Release of PHP 8.4 |
|--------------------|--------------------|
| June 6, 2024       | Alpha 1            |
| June 20, 2024      | Alpha 2            |
| July 4, 2024       | Alpha 3            |
| July 16, 2024      | Feature freeze     |
| July 18, 2024      | Beta 1             |
| August 1, 2024     | Beta 2             |
| August 15, 2024    | Beta 3             |
| August 29, 2024    | RC 1               |
| September 12, 2024 | RC 2               |
| September 26, 2024 | RC 3               |
| October 10, 2024   | RC 4               |
| October 24, 2024   | RC 5               |
| November 7, 2024   | RC 6               |
| November 21, 2024  | GA                 |

## Install and test PHP 8.4 on macOS

1. Install the [Homebrew package manager](https://brew.sh) if it's not done already.
2. Run `brew update` to make sure Homebrew and the formulae are up to date.
3. Add a new tap (basically a GitHub repository) for PHP 8.4's formula: `brew tap shivammathur/php`.
4. Install the pre-compiled binary for PHP 8.4 (also called "a bottle" in Homebrew's context). This will make the install so much faster. `brew install php@8.4`.
5. Link it to make sure that the `php` alias targets the right binary: `brew link --overwrite --force php@8.4`.

If you want to learn more about how to install PHP on your Mac, I wrote something for you: [PHP for Mac: get started fast using Laravel Valet](https://benjamincrozat.com/install-php-mac-laravel-valet)

## What's new in PHP 8.4

### PHP 8.4's DOM extension now supports HTML5

PHP 8.4's DOM extension just got a big upgrade with support for HTML5 parsing and serialization. This means no more headaches when dealing with HTML5 specific tags or embedding HTML in your JavaScript.

Just use the new `DOM\HTMLDocument` class and your HTML5 content will be handled correctly, keeping up with the modern web standards.

Here's how you create an HTML document from a string:

```php
use DOM\HTMLDocument;

$htmlDocument = HTMLDocument::createFromString('<!DOCTYPE html><html><body>Hello, HTML5!</body></html>');
```

Or from a file:

```php
use DOM\HTMLDocument;

$htmlDocument = HTMLDocument::createFromFile('path/to/your/file.html');
```

Learn more: [PHP RFC: DOM HTML5 parsing and serialization](https://wiki.php.net/rfc/domdocument_html5_parser)

### PHP 8.4 comes with an increased bcrypt cost by default

**In PHP 8.4, the default cost of [bcrypt](https://en.wikipedia.org/wiki/Bcrypt#:~:text=bcrypt%20is%20a%20password%2Dhashing,presented%20at%20USENIX%20in%201999.) has been increased to 12.** What does that even mean?

Bcrypt is the password hashing function that PHP uses. It acts as a shield against hackers who would want to crack passwords.

The strength of this shield can be adjusted. The higher the setting or the "cost", the stronger the shield because bcrypt is an adaptive function: *"over time, the iteration count can be increased to make it slower, so it remains resistant to brute-force search attacks even with increasing computation power."*

And why is it such a big deal? Because increasing the cost of bcrypt makes password hashing a few milliseconds slower.

Learn more: [PHP RFC: Increasing the default BCrypt cost](https://wiki.php.net/rfc/bcrypt_cost_2023)

### PHP 8.4 can parse large XML documents more reliably

**This change resolved a potential issue in the ext/xml PHP extension involving its handling of large XML document parsing.**

Conflicting modifications in libxml2 version 2.7.0 unintentionally disrupted large document parsing when using `xml_parse()` and `xml_parse_into_struct()` functions, resulting in a parsing error.

PHP 8.4 introduced a new parser option to properly handle these large XML documents and prevent the parsing error, making it possible for developers to parse large XML documents effectively, without needing complex workarounds.

Learn more: [PHP RFC: XML_OPTION_PARSE_HUGE](https://wiki.php.net/rfc/xml_option_parse_huge)