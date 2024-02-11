---
Image: 
Title: Understanding jQuery's `.each()` method
Description: Learn how to use jQuery's `.each()` method to iterate over DOM elements and arrays, and discover a modern vanilla JavaScript alternative.
Canonical: 
Audio:
Published at:
Modified at:
Categories: javascript, jquery
---

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

Let's say we want to add a class to every `<p>` tag on our page. Here's how easy it is with `jquery each`:

```js
$('detail').each(function() {
    $(this).setAttribute('open', true);
});
```

Simple, right? But what if I told you that you could achieve the same thing without jQuery, using just vanilla JavaScript?

## Modern Vanilla JavaScript alternatives

As web development evolves, so does JavaScript. The modern ECMAScript standards have introduced methods that make DOM manipulation just as straightforward as jQuery once did. For instance, to replicate jQuery's `each` method example, you can use `forEach` on a NodeList:

```js
document.querySelectorAll('p').forEach(function(el) {
  el.classList.add('new-class');
});
```

Here, `querySelectorAll` returns a NodeList of all `<p>` tags, which we then iterate over with `forEach`, adding the class to each element.

## Conclusion

While jQuery's `.each()` method offers a simple and effective way to iterate over elements, modern JavaScript provides equally powerful alternatives. As developers, staying updated with these advancements allows us to write cleaner, more efficient code. Whether you're a jQuery enthusiast or a vanilla JavaScript advocate, understanding both approaches enhances your toolkit for web development challenges.