---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/177/oe6qFaj4OtlL8ptcQwWgoxtf5GVXIg-metaNjkzLmpwZw%3D%3D-.jpg
Title: Easily convert a PHP array to JSON
Description: Convert PHP arrays to JSON with `json_encode()`. Ideal for data exchange, storing data, and API communication.
Published at: 2023-09-16
Modified at: 
Categories: php
---

## Transforming PHP arrays to JSON

**To convert a PHP array to JSON, you can use the [`json_encode()`](https://www.php.net/json_encode) function. Here's how it's done:**

```php
<?php

$array = [
    "foo" => "bar", 
    "baz" => "qux",
];

$json = json_encode($array);

echo $json;
```

Running the above code snippet will output: `{"foo":"bar","baz":"qux"}`. And just like that, your PHP array is now a JSON string!

Let's unwrap the mystique around `json_encode()`: 

- `json_encode()` is a function in PHP that converts a PHP value into a JSON value. This can be done for PHP values such as arrays, objects, and even simple data types like strings, booleans, and integers.
- JSON is an acronym for JavaScript Object Notation, but don't let the name fool you - it can be used beyond JavaScript. It's a lightweight data-interchange format that's easy for humans to read and write and easy for machines to parse and generate.

## When to transform a PHP array to JSON

Here are some of the use cases I met where you would need to convert PHP arrays to JSON format:

- **Data exchange**: You may need to convert PHP arrays to JSON when exchanging data between a server and a web application. JSON is the common standard for such data exchange (for JSON was invented, it was XML).
- **Storing data**: Since JSON is a lightweight and readable format, it's commonly used to store complex data structures, especially when you want to maintain the data hierarchy.
- **Work with modern APIs**: Most modern APIs such as those for social media platforms and cloud services communicate using JSON, so converting your PHP array to JSON can be necessary to work with these APIs.

## Catching JSON errors

PHP also provides a function to inspect the last occurred error during JSON encoding/decoding. 

```php
<?php

$array = [
    "foo" => "bar", 
    "baz" => "qux",
];

$json = json_encode($array);

if (json_last_error() !== JSON_ERROR_NONE) {
    echo json_last_error_msg();
}
```

If something unexpected happens during the JSON encoding, you can get the error messages with [`json_last_error_msg()`](https://www.php.net/json_last_error_msg).

But this is an old-fashioned way of doing it if you ask me. You could also simply ask PHP to throw an exception when something goes wrong using the [`JSON_THROW_ON_ERROR`](https://www.php.net/manual/en/json.constants.php#constant.json-throw-on-error) constant:

```php
try {
    $array = [
        "foo" => "bar", 
        "baz" => "qux",
    ];

    $json = json_encode($array, JSON_THROW_ON_ERROR);
} catch (JsonException $exception) {
    exit($exception->getMessage());
}
```