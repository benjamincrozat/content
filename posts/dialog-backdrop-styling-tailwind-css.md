---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/214/qrkEYddhnRpmuUVrqz10PO89Zc6pnA-metaYmFja2Ryb3AtdGFpbHdpbmQtY3NzLmpwZw%3D%3D-.jpg
Title: Style an HTML <dialog>'s backdrop with Tailwind CSS
Description: Discover how to style an HTML dialog's backdrop using Tailwind CSS.
Canonical: 
Audio:
Published at: 2023-11-02
Modified at: 
Categories: tailwind-css
---

**To style a native HTML dialog's backdrop, use the `backdrop:` modifier introduced in Tailwind CSS 3.1.**

```html
<dialog class="backdrop:bg-black/50 backdrop:backdrop-blur-md">
	<p>Lorem ipsum dolor sit amet.</p>
</dialog>
```

(Using the class to add a backdrop filter to the dialog's backdrop is a bit weird, but it works!)

I was surprised to see how well this relatively new dialog HTML element is supported.

At the time I'm writing these lines, the `<dialog>` element is supported by:
- Firefox 98+
- Firefox for Android 118+
- Google Chrome 37+
- Google Chrome for Android 128+
- Opera 24+
- Safari/Mobile Safari 15.4+

[Check out the support chart on Can I use](https://caniuse.com/dialog).

Also, [I made a working CodePen](https://codepen.io/benjamincrozat/pen/poGERgV) for those curious to see how all this works.