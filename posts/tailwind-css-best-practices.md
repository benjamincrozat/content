---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/benjamincrozat/content/assets/3613731/c8acd112-e05e-4d07-8f66-71a5a5d8f078
Title: 6 Tailwind CSS best practices, tips, and tricks for 2024
Description: Tailwind CSS is a beloved CSS framework that has been my go-to since 2018. Let me share my knowledge and insights coming from years of experience.
Canonical:
Audio:
Published at: 2023-12-22
Modified at:
Categories: css, tailwind-css
---

## Introduction to Tailwind CSS best practices, tips, and tricks

[Tailwind CSS](/tailwind-css) is my go-to CSS framework since 2018. I didn't use anything else since then, seriously!

Therefore, I think I'm in the right position to teach a thing or two to people who also fell in love with it.

## Extend Tailwind CSS using the configuration file, not custom CSS

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

## Use Visual Studio Code plugins to work more efficiently with Tailwind CSS

### Tailwind CSS IntelliSense

Tailwind CSS IntelliSense is an official plugin made by Tailwind Labs that helps every developer work more efficiently with the framework by adding features like autocomplete, syntax highlighting, and linting.

A must-have!

[Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss) on the Visual Studio Code marketplace.

### Inline Fold

If you feel overwhelmed by the amount of classes in your HTML, you might want to collapse the `class` attribute for improved clarity.

Inline Fold is a plugin for Visual Studio Code that solves this problem really well.

[Inline Fold](https://marketplace.visualstudio.com/items?itemName=moalamri.inline-fold) on the Visual Studio Code marketplace.

## Use line breaks

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

## Extract to a component

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

## Don't extract to a parent class. Leverage editor and language features instead.

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
