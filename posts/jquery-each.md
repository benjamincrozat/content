---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/benjamincrozat/content/assets/3613731/71b3175d-790d-4206-988c-c80a7c79ed8b
Title: Understanding jQuery's `.each()` method
Description: Learn how to use jQuery's `.each()` method to iterate over DOM elements and arrays, and discover a modern vanilla JavaScript alternative.
Canonical: 
Audio:
Published at: 2024-02-11
Modified at:
Categories: javascript, jquery
---

## Introduction to jQuery's `.each()` method

Ah, jQuery. It's been a cornerstone of web development for years, offering a simplified way to manipulate the DOM, handle events, and perform AJAX requests. One of its most beloved features? The `.each()` method. This little gem allows developers to iterate over both arrays and DOM elements effortlessly, applying functions to each item in the set.

## Syntax and usage

jQuery's `each` method has a straightforward syntax. It takes a function as an argument, which is executed for each item in the set. Here's a quick look:

```js
$('selector').each(function(index, element) {
    // Your code goes here
});
```

In this snippet, `selector` targets the DOM elements you want to iterate over. The function then receives two arguments: `index`, the position of the current item in the set, and `element`, the item itself.

## Practical example

Let's say we want a Frequently Asked Questions section with only one question open at a time:

```js
$('summary').click(function () {
    var parent = $(this).parent('details');
  
    $('details').each(function () {
        if (! $(this).is(parent)) {
            $(this).removeAttr('open');
        }
    });
});
```

Not that hard, right? The `.each()` method comes in handy to find all the details elements and close them, excluding the one we clicked in.

But what if I told you that you could achieve the same thing without jQuery, using just vanilla JavaScript?

## The equivalent in Vanilla JavaScript

As web development evolves, so does JavaScript. The modern ECMAScript standards have introduced methods that make DOM manipulation just as straightforward as jQuery once did. For instance, to replicate jQuery's `each` method example, you can use `forEach` on a `NodeList`.

Here's our practical example from above, but using Vanilla JavaScript:

```js
document.querySelectorAll('summary').forEach(function(summary) {
    summary.addEventListener('click', function() {
        var parent = this.parentNode;

        document.querySelectorAll('details').forEach(function(details) {
            if (details !== parent) {
                details.removeAttribute('open');
            }
        });
    });
});
```

Here, `querySelectorAll` returns a `NodeList` of all `<details>` tags, which we then iterate over with `forEach`, removing the `open` attribute from each `<details>` elements besides the one we clicked on.

## Conclusion

While jQuery's `.each()` method offers a simple and effective way to iterate over elements, modern JavaScript provides equally powerful alternatives. As developers, staying updated with these advancements allows us to write cleaner, more efficient code. Whether you're a jQuery enthusiast or a vanilla JavaScript advocate, understanding both approaches enhances your toolkit for web development challenges.
