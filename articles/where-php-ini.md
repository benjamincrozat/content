---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/220/LZtkGaaS3mnQXxCBhxVWOVfrezhHWA-metaQnVzaW5lc3MgdGVhbSBsb29raW5nIGZvciBuZXcgcGVvcGxlLmpwZw%3D%3D-.jpg
Title: This is where your php.ini file is
Description: Discover the location of your php.ini file using two simple methods: the phpinfo() function or the command line.
Canonical: 
Published at: 2023-11-02
Modified at: 
Categories: php
---

Your *php.ini* file is the control center for setting up your environment. Here are straightforward methods to locate this file.

## phpinfo() tells you where your php.ini file is

The quickest path any PHP developer discovers first is through the `phpinfo()` function. It’s a simple process:

- Create a new project with a PHP file named *index.php*.
- Add the following code:
```php
<?php
phpinfo();
?>
```
- Open the project in your web browser.

The "Loaded Configuration File" section will indicate where the active php.ini file is.

![phpinfo() in action.](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/216/conversions/JAyCkwTofAYGl4PX3byMXdOJ8DUTcQ-metaQ2xlYW5TaG90IDIwMjMtMTEtMDIgYXQgMTcuMDQuNTBAMngucG5n--medium.jpg)

## The command line can also find where you php.ini file is

For those who favor the command line, PHP provides a straightforward command:
1. Open the terminal.
2. Type `php --ini` and execute it.
3. The terminal will display the path to the *php.ini* file.

![Using a terminal to run the php --ini command.](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/218/conversions/IdaI8uqocUu45gmvwzENy2KOGSiec2-metaQ2xlYW5TaG90IDIwMjMtMTEtMDIgYXQgMTcuMTIuNTRAMngucG5n--medium.jpg)