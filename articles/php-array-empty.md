---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/12/confused_xxboi4.jpg
Title: Is your PHP array empty? A few ways to make sure of it.
Description: There are multiple ways to check if an array is empty. Let me tell you about each of them and why and when you should use them.
Published at: 2022-10-09
Modified at: 2022-11-23
Categories: php
---

## Introduction

To ensure that a PHP array is empty, you can use any of the following methods:

1. Use the `empty()` function to check if the array is empty and return a boolean value.
2. Use the `count()` (or `sizeof()`) function to count the number of elements in the array and check if it is equal to zero.
3. Use the not operator (`!`). If the array does hold any value, the not operator will return `true`.

## The `empty()` function

The `empty()` function determines if a value is empty or not. It simply returns `true` if it's empty, or `false` if it's not.

This is my favorite way to check if an array is empty in PHP.

```php
$foo = [];

// true
if (empty($foo)) {
    //
}

$bar = ['Foo', 'Bar', 'Baz'];

// false
if (empty($bar)) {
    //
}
```

Learn more about the [`empty()`](https://www.php.net/empty) function.

## The `count()` function

The `count()` function counts the number of entries in an array and returns it as an integer.

You can even use it with [Countable](https://www.php.net/manual/en/class.countable.php) objects.

```php
echo count(['Foo', 'Bar', 'Baz']);
```

For multidimensional arrays, there's a second parameter for which you can use the `COUNT_RECURSIVE` constant to recursively count the numbers of items.

```php
$array = [
    'Foo' => [
        'Bar' => ['Baz'],
    ],
];

$count = count($array, COUNT_RECURSIVE);

// If $count is greater than zero, then your array is not empty.
if ($count > 0) {
    //
}
```

Learn more about the [`count()`](https://www.php.net/count) function.

## The `sizeof()` function

`sizeof()` is an alias of count(). [PHP actually has a lot of aliases for various functions](https://www.php.net/manual/en/aliases.php).

There's nothing to add, [you already know how to use it](#the-count-function):

```php
echo sizeof(['Foo', 'Bar', 'Baz']);
```

Learn more about the [`sizeof()`](https://www.php.net/sizeof) function.

## The not (`!`) operator

This one is simple. You are probably used to the not (`!`) operator. I didn't know it could check for empty arrays, but here I am, after 15 years of PHP learning yet another basic thing.

```php
$foo = [];

if (! $foo) {
    echo '$foo is empty.';
}
```

