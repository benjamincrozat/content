---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/25/tailwind-css_uoqpuu.png
Title: Tailwind CSS: the ultimate guide to get started
Description: This is the most comprehensive tutorial about Tailwind CSS. Learn how to make front-end development great again.
Canonical: 
Audio:
Published at: 2022-12-25
Modified at: 2024-07-17
Categories: css, tailwind-css
---

## Introduction

I've been using Tailwind CSS since 2018 in a plethora of projects. I only wrote a few lines of traditional CSS since then. Once I got the hang of Tailwind CSS, I couldn't go back. So naturally, I have **a lot** to say about it and I hope you will find this big article helpful!

**And by the way, if this isn't enough, I can recommend you "[Level up with Tailwind CSS](recommends/level-up-tailwind-css)" from Shruti Balasa, which is way more skilled at Tailwind CSS and CSS in general than I am. You won't reget it.**

## What is Tailwind CSS?

**[Tailwind CSS](https://tailwindcss.com) is a framework designed around the utility-first philosophy.**

Instead of writing classic CSS, it encourages you to combine multiple classes to create the desired appearance.

Tailwind CSS was created back in 2017 by Adam Wathan and Steve Schoger.

Here's how we used to style buttons since the beginnings: 

```css
.btn {
    background-color: blue;
    color: white;
    padding: 1rem;
}
```

Here's how Tailwind CSS helps you to do it:

```html
<button class="bg-blue-400 p-4 text-white">
    Click me
</button>
```

## Is Tailwind CSS free?

**Yes, Tailwind CSS free is 100% free.**

You can even contribute to it yourself on [official repository](https://github.com/tailwindlabs/tailwindcss), because it's open source.

You might have heard about the commercial products built around the framework. But these are completely optional, you will never need them.

## Tailwind CSS makes you love front-end development

[Tailwind CSS](https://tailwindcss.com) comes with the following benefits:
- You will say goodbye to unused styles;
- You will never end up with 4,394 different `color`, `margin`, or `z-index` values;
- You won't have to bother with best practices that nobody in your team wants to follow.

With that, speed of execution will be increased, and you'll enjoy crafting user interfaces again.

![Tailwind CSS](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/118/conversions/Screenshot_2022-12-25_at_16.11.53_b6pkht-medium.jpg)

## Tailwind CSS VS. Bootstrap 5

In short, [Tailwind CSS](https://tailwindcss.com) is a utility-first CSS framework, and [Bootstrap 5](https://getbootstrap.com) is mainly a collection of UI components.

Comparing Tailwind CSS to Bootstrap is like comparing apples to cars; it doesn't make sense.

Bootstrap is more than a bunch of utility CSS classes. It provides a ton of excellent UI components that make use of JavaScript. Therefore, it has a larger footprint.

*When used the right way*, Tailwind CSS is extremely small (especially after compression).

Both are highly customizable.

Tailwind CSS will better fit teams that strongly value user interfaces.

![Tailwind CSS VS. Bootstrap](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/119/conversions/comparison_esionn-medium.jpg)

## Who uses Tailwind CSS?

The list of big companies using Tailwind CSS is quite impressive.

Some of them fully use the framework, while others do a weird blend.

And if you take a look at their code, you can see how they customize Tailwind CSS to their needs.

Here are few of them:

- GitHub, for their [research website](https://githubnext.com)
- Google, for their [I/O 2022 conference website](https://io.google/2022/)
- Laravel, for the [Laracon Online website](https://laracon.net)
- [Loom](https://www.loom.com)
- [Mashable](https://mashable.com)
- [Microsoft .NET](https://dotnet.microsoft.com/en-us/)
- NASA, for their [Jet Propulsion Laboratory website](https://www.jpl.nasa.gov)
- Netflix, for their [global top 10 microsite](https://top10.netflix.com)
- [SavvyCal](https://benjamincrozat.com/recommends/savvycal)
- [Shopify](https://www.shopify.com)
- [The Verge](https://www.theverge.com)

See more on [the official website of Tailwind CSS](https://tailwindcss.com/showcase).

## Tailwind Play: a CodePen-like for quick prototyping

[Tailwind Play](https://play.tailwindcss.com) is the best tool to focus on quickly crafting a piece of UI right from your browser.

It's a straightforward web application with the following features:
- An HTML editor with great autocompletion (including every class from the framework)
- A CSS editor
- A config editor
- A magic button to reformat your code
- A version switcher to use an experimental or an older version of the framework
- A layout switcher
- A light and dark mode switcher

That's it, and that's all you need to get started with Tailwind CSS.

You can jump to the last part of this tutorial, where we'll craft a UI element to get the hang of the framework.

![Tailwind Play](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/120/conversions/Screenshot_2022-12-25_at_16.13.19_ssohln-medium.jpg){: width="1280" height="720"}

## Tailwind Play CDN is convenient and unlike others

Tailwind Play CDN is not the typical CDN that serves a static file. It parses your HTML and injects the corresponding CSS into a `<style>` tag.

This is a great way to prototype any idea you have.

1. Create a *index.html* file.
2. Paste this code:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
    
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
    <h1 class="text-3xl font-bold underline">
        Hello, world!
    </h1>
</body>
</html>
```

Et voilà!

I recommend using something other than it in production, as your performances may suffer.

## How to set up Tailwind CSS in your project

Ultimately, Tailwind CSS is just a collection of styles. It can be integrated into *any* project.

For instance, the official website shows [how to use Tailwind CSS with its CLI tool](https://tailwindcss.com/docs/installation).

Or using PostCSS: https://tailwindcss.com/docs/installation/using-postcss.

And even apps that use Vite for processing and serving assets: https://tailwindcss.com/docs/guides/vite

You may also be interested in how to integrate Tailwind CSS inside a Laravel project that uses Vite (like this very blog): https://tailwindcss.com/docs/guides/laravel

Or if you're still using Mix: https://tailwindcss.com/docs/guides/laravel#mix

## Watch videos, the best way to learn Tailwind CSS

Videos are a great way to learn a new technology. There are plenty of free courses over the web, and they're one Google search away from you.

That said, there are some I would recommend to anyone that's not familiar with the framework.

First, Laracasts offers a *free* course called [HTML and CSS workshop](https://laracasts.com/series/html-and-css-workshop) using Tailwind CSS.

Tailwind CSS even has an [official YouTube channel](https://www.youtube.com/@TailwindLabs).

They provide great videos showing off how to build useful UI components like "[Building a command palette with Tailwind CSS, React, and Headless UI](https://www.youtube.com/watch?v=-jix4KyxLuQ)" or what could be your assignment at your job: "[Translating a Custom Design System to Tailwind CSS](https://www.youtube.com/watch?v=cZc4Jn5nK3k)".

## Ask for help on the official forum

Tailwind CSS has an [official forum](https://github.com/tailwindlabs/tailwindcss/discussions) on GitHub. Feel free to ask about everything you're unable to find on the [documentation](https://tailwindcss.com/docs).

![Tailwind CSS forum on GitHub](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/122/conversions/Screenshot_2022-12-26_at_10.27.31_e8x0ye-medium.jpg){: width="1280" height="720"}

## Best practices to keep everything organized

### Extend Tailwind CSS using the configuration file, not custom CSS

Tailwind CSS lets you customize a lot of things by simply editing the *tailwind.config.js* file.

For example, if you want to add a new color, you can extend the default theme to add your own set of values:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
    theme: {
        extend: {
            colors: {
                brand: '#abc123',
            },

            fontFamily: {
                handwriting: ['Some hanwriting font'],
            }
        }
    }
}
```

By leveraging the configuration file properly, tons of classes and their variants will be automatically generated for you like `bg-brand`, `text-brand`, `border-brand`, `hover:bg-brand`, etc.

[Learn more](https://tailwindcss.com/docs/theme) on the official documentation.

### Use Visual Studio Code plugins to work more efficiently with Tailwind CSS

#### Tailwind CSS IntelliSense

Tailwind CSS IntelliSense is an official plugin made by Tailwind Labs that helps every developer work more efficiently with the framework by adding features like autocomplete, syntax highlighting, and linting.

A must-have!

[Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) on the Visual Studio Code marketplace.

#### Inline Fold

If you feel overwhelmed by the amount of classes in your HTML, you might want to collapse the `class` attribute for improved clarity.

Inline Fold is a plugin for Visual Studio Code that solves this problem really well.

[Inline Fold](https://marketplace.visualstudio.com/items?itemName=moalamri.inline-fold) on the Visual Studio Code marketplace.

### Use line breaks

Let's say you have a button that looks like this:

```html
<button class="bg-gradient-to-r from-indigo-300 dark:from-indigo-500 to-indigo-400 dark:to-indigo-600 font-semibold px-4 sm:px-6 py-2 rounded shadow-lg text-sm text-white w-full">
    Click me
</button>
```

One easy trick to make more readable is to break the `class` attribute to multiple lines:

```html
<button
	class="bg-gradient-to-r from-indigo-300 dark:from-indigo-500
    to-indigo-400 dark:to-indigo-600 font-semibold px-4 sm:px-6
    py-2 rounded shadow-lg text-sm text-white w-full"
>
    Click me
</button>
```

### Extract to a component

Extracting your button to a component (Blade, React, Vue, or whatever you like) will drastically clean up your files.

Here's a Blade template file using a `button` component containing the same code as above:

```blade
<!DOCTYPE html>
<html>
	<head>
		…
	</head>
	<body>
		…
		
		<x-button>
			Book me
		</x-button>
		
		…
	</body>
</html>
```

### Don't extract to a parent class. Leverage editor and language features instead.

Extracting a bunch of Tailwind CSS classes to a parent class is tempting.

```css
.btn {
    @apply bg-gradient-to-r from-blue-400 to-blue-300 px-4 py-3 rounded
}
```

However, this completely defeats the purpose of Tailwind CSS, which is to have a single source of truth and make things easier to manage.

Instead, use your editor's multi-cursor feature and create sub-components thanks to whatever templating engine you use.

Here's an example written using Laravel's Blade templating engine:

```blade
{{-- Somewhere in your views… --}}
<x-primary-btn>
    Click me
</x-primary-btn>

{{-- primary-btn.blade.php --}}
<x-btn class="bg-gradient-to-r from-blue-400 to-blue-300 text-white">
    {{ $slot }}
</x-btn>

{{-- btn.blade.php --}}
<button {{ $attributes->merge(['class' => 'bg-gray-200 px-4 py-3 rounded']) }}>
    {{ $slot }}
</button>
```

1. We begin with a base `btn` component with a gray rounded `button` that is enough for most cases.
2. Then, we have a `primary-btn` component that extends the `btn` component and adds a blue gradient background and white text. This component can be used for call-to-action buttons.

## Do more with the official plugins

### The container queries plugin

Instead of using media queries and viewport sizes to change an element's layout, we can rely on the size of its container.

Here's all about container queries on CSS-Tricks: [Say Hello to CSS Container Queries](https://css-tricks.com/say-hello-to-css-container-queries/)

The container queries plugin provides a convenient way to handle them in a Tailwind CSS fashion.

```html
<div class="@container">
    <div class="@lg:underline">
		<!-- This text will be underlined when the container is larger than `32rem` -->
	</div>
</div>
```

[Read the official documentation on GitHub.](https://github.com/tailwindlabs/tailwindcss-container-queries)

### The forms plugin

The forms plugin is maintained by the team from Tailwind CSS. It resets forms to a consistent state across all browsers and makes them easily stylable.

Learn more: [Tailwind CSS forms plugin: a step-by-step guide](https://benjamincrozat.com/tailwind-css-forms-plugin)

### The typography plugin

![Tailwind CSS typography plugin.](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/126/conversions/Screenshot_2022-12-28_at_15.11.26_ysda6j-medium.jpg)

The typography plugin contains tons of styles, that you can customize, for written content. It's extremely well done and useful.

You're actually witnessing those styles on this blog post.

```html
<article class="prose lg:prose-xl">
    <!-- Parsed Markdown -->
</article>
```

[Read the official documentation.](https://tailwindcss.com/docs/typography-plugin)

## Plenty of Tailwind CSS examples can be copied and pasted. No design skills required.

Due to its utility-first philosophy, Tailwind CSS allows to copy and paste fully-designed components into any website.

This is one of its strengths and you can experiment with components libraries right now. I compiled a list of free and paid ones.

### Free libraries

- [daisyUI](https://daisyui.com)
- [Flowbite](https://flowbite.com/docs/getting-started/introduction/)
- [tailwindcomponents.com](https://tailwindcomponents.com)

### Paid libraries

- [Tailwind Elements](https://tailwind-elements.com)
- [Tailwind UI](https://tailwindui.com)
- [Tailwind UI Kit](https://tailwinduikit.com)

## Tailwind CSS alternatives

As with everything in life, there are alternatives.

Keep in mind we are looking for purely utility-first CSS frameworks. UI frameworks like [Bootstrap actually have utility classes](https://getbootstrap.com/docs/5.3/utilities/background/), and you can use them if you like.

These frameworks below can be integrated into any project based on any JavaScript framework (Ember, React, Svelte, Vue.js, etc.).

- [Basscss](https://basscss.com/)
- [Expressive CSS](https://johnpolacek.github.io/expressive-css/)
- [shed.css](https://tedconf.github.io/shed-css/)
- [turretcss](https://turretcss.com)

