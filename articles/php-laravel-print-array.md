---
Author: Benjamin Crozat
Title: Learn how to print an array with PHP (+ Laravel)
Description: Debugging requires dissecting everything. Here's a list of all the one-line of code built-in ways to print arrays in PHP (and even Laravel-specific helpers).
Published at: 2022-10-07
Modified at: 
Categories: php, laravel
---

## Introduction

**There are multiple ways to print the content of an array in PHP.**

This article will review each of them built into the language.

## In PHP

### print_r()

print_r() displays arrays in an human-readable format.

Example:

```php
print_r(['Foo', 'Bar', 'Baz']);
```

Output:

```
Array
(
    [0] => Foo
    [1] => Bar
    [2] => Baz
)
```

If you need to capture the output, you can pass a second parameter to print_r():

```php
$output = print_r(['Foo', 'Bar', 'Baz'], true);
```

### var_dump()

var_dump() prints informations about any type of value. It works great for arrays as well!

Example:

```php
var_dump(['Foo', 'Bar', 'Baz']);
```

Output:

```
array(3) {
  [0]=>
  string(3) "Foo"
  [1]=>
  string(3) "Bar"
  [2]=>
  string(3) "Baz"
}
```

You can also print multiple variables at once:

```php
var_dump($foo, $bar, $baz, …);
```

### var_export()

var_export() prints a parsable string representation of a variable. It means you could just copy and paste it into your source code.

Example:

```php
$array = ['Foo', 'Bar', 'Baz'];

var_export($array);
```

Output:

```
array (
  0 => 'Foo',
  1 => 'Bar',
  2 => 'Baz',
)
```

### json_encode()

`json_encode()` prints can print arrays as JSON.

Example:

```php
$array = ['Foo', 'Bar', 'Baz'];

echo json_encode($array);
```

Output:

```
["Foo","Bar","Baz"]
```

## In Laravel

### dump()

![dump()](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/86/conversions/Screen_Shot_2023-01-16_at_07.54.59_ichkqp-medium.jpg){: width="400"}

The `dump()` function prints in details arrays containing any value.

```php
$array = ['Foo', 'Bar', 'Baz'];

dump($array);
```

It also accepts an infinity of arguments:

```php
dump($a, $b, $c, $d, $e, …);
```

### dd()

The `dd()` function does the same thing as `dump()`, but stops code execution.

```php
$array = ['Foo', 'Bar', 'Baz'];

dd($array);
```

It also accepts an infinity of arguments:

```php
dd($a, $b, $c, $d, $e, …);
```

