---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/benjamincrozat/content/assets/3613731/c0389eff-b948-496b-94c5-06b10d4c39ce
Title: Get started with jQuery in 5 minutes
Description: Dive into the basics of jQuery, learn how to include it in your project, and create your first component in just a few minutes.
Canonical: 
Audio:
Published at: 2024-02-12
Modified at: 
Categories: javascript, jquery
---

## Introduction to jQuery

[jQuery](https://jquery.com) is a fast, small, and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, and animation much simpler with an easy-to-use API that works across a multitude of browsers (especially the old ones).

Nowadays, we might think jQuery has been long dead, but it's not. It's still the dominant JavaScript framework and the big majority of web developers are using it.

Therefore, why wouldn't I write articles about it?

## Include jQuery in your HTML using the official CDN

To start using jQuery in your web projects, you first need to include it in your HTML. The easiest way to do this is by using the official Content Delivery Network (CDN). Simply add the following script tag in the `<head>` section of your HTML document:

```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
```

The team team behind jQuery doesn't recommend using an URL that always point to the latest version of the framework for [various reasons](https://blog.jquery.com/2014/07/03/dont-use-jquery-latest-js/).

## Create your first jQuery component

Now that you've included jQuery, let's create a simple component: a button that hides itself when clicked. Add the following HTML and jQuery script to your document:

```html
<button id="hideButton">Hide me!</button>
```

```javascript
$(document).ready(() => {
  $('#hideButton').click(() => {
    $(this).hide();
  });
});
```

This code uses jQuery to attach a click event to the button with the ID "hideButton". When the button is clicked, jQuery's `hide()` method is called on the element, making it disappear from the page.

## Conclusion

That's it! You've now seen how jQuery can make JavaScript programming easier and more intuitive, especially for tasks like manipulating HTML elements and handling events. Start experimenting with more components and explore the vast possibilities jQuery offers.
