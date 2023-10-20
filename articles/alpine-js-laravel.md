---
Title: Add Alpine.js to any Laravel project
Description: Alpine.js is a great companion for a Laravel app. Let's see how you can add it in any project.
Published at: 2023-10-13
Modified at: 2023-10-20
Categories: alpine-js, javascript, laravel
---

## Introduction

[Alpine.js](https://alpinejs.dev) is a great way to start adding reactivity to your user interface. [I wrote about this minimalist framework](/alpine-js) if you are not familiar with it yet.

Today, we will learn how to add Alpine.js into an existing Laravel project. Of course, this will even work on new projects. Let's dive in!

## Use Alpine.js via a CDN

Alpine.js is such a simple framework that it can just be dropped in any web page using the CDN of your choice.

```html
<!DOCTYPE html>
<html>
	<head>
		…

		<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
	</head>
	<body>
		…
	</body>
</html>
```

That's it. And you can even add plugins that way:

```html
<!DOCTYPE html>
<html>
	<head>
		<script defer src="https://cdn.jsdelivr.net/npm/@alpinejs/intersect@3.x.x/dist/cdn.min.js"></script>
		<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
	</head>
	<body>
		…
	</body>
</html>
```

You could already stop reading this article. If you are missing the good old days when everybody used jQuery and build tools were only for hipsters, you should be happy!

**Pro tip: the URLs in this example redirect to the last version of the framework and plugin. Replace them by the target URL instead.**

## Install Alpine.js via NPM, Yarn, pnpm, or Bun

If you'd like to control the amount of HTTP requests on your page and don't fear compilation processes, you might instead bundle the framework into your JavaScript.

Whatever package manager you use (NPM, Yarn, pnpm, or Bun), use the following command.

If you use NPM:

```bash
npm install alpinejs
```

If you use Yarn:

```bash
yarn add alpinejs
```

If you use Bun:

```bash
bun add alpinejs
```

## Set up Alpine.js

Now, we must import Alpine and create an instance of the framework.

In *resources/js/app.js*, make the following modifications:

```js
import Alpine from 'alpinejs'

Alpine.start()

// If you want Alpine's instance to be available everywhere.
window.Alpine = Alpine
```

That's it. Simple, right?

Oh, before I forget, here's how to use plugins. First, install one.

If you use NPM:

```bash
npm install @alpinejs/intersect
```

If you use Yarn:

```bash
yarn add @alpinejs/intersect
```

If you use Bun:

```bash
bun add @alpinejs/intersect
```

Then, tell Alpine to use the Intersect plugin:

```js
import Alpine from 'alpinejs'
import Intersect from '@alpinejs/intersect'

Alpine.plugin(Intersect)

Alpine.start()

window.Alpine = Alpine
```

## Add minimal Alpine.js code

We're almost there!

Include your JavaScript using the `@vite` directive and copy and paste this basic component:

```blade
<!DOCTYPE html>
<html>
	<head>
		…
		
		@vite(['resources/js/app.js'])
	</head>
	<body>
		<div x-data="{ count: 0 }">
			<button @click="count++">Add</button>
			<span x-text="count">0</span>
		</div>
	</body>
</html>
```

Yes, this is an old-fashioned counter to demonstrate that the framework is working.

I know, very original, right? 😅

## Compile your assets and check your browser

If you did everything correctly, Alpine.js should now be up and running. Compile your assets and check your browser!

If you use NPM:

```bash
npm run dev
```

If you use Yarn:

```bash
yarn dev
```

If you use Bun:

```bash
bun run dev
```

Done! Now, go build something amazing!
