---
Image: https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/68/NZbLqdyKKjVodLp6Yesr1iBA50Vk3K-metacGFja2FnZS1tYW5hZ2VyLmpwZw%3D%3D-.jpg
Title: Bun vs. NPM, Yarn, pnpm, and others
Description: Learn why Bun is a great and can be used as a package manager, replacing NPM, Yarn, pnpm, and others.
Published at: 2023-09-11
Modified at: 
Categories: javascript
---

## What is Bun?

**[Bun](https://bun.sh) is a fast JavaScript all-in-one toolkit.** It can be used as a runtime (a drop-in replacement much faster than Node.js), as a test runner, and even as a package manager. Which is what interests us today.

Unlike Node.js or Deno, Bun is built on top of [Webkit](https://webkit.org)'s JavaScript engine (JavaScriptCore). Webkit is the basis for Mobile Safari on Apple's mobile platforms, as well as Safari for Mac.

## Why would you switch away from NPM, pnpm, or Yarn?

Why would you take some time to switch to Bun instead of sticking with a regular Node.js runtime?

Well, if you actually test Bun, you will notice how incredibly faster than Node.js it is. **Up to 30x!**

1. Your front-end dependencies will install faster.
2. Your assets will compile faster.
3. Your continuous integration environment will also run faster since installing and compiling front-end dependencies takes less time.

## How to install Bun on macOS using Homebrew

Installing Bun on macOS couldn't be easier. Just add the new source using `brew tap oven-sh/bun` and install Bun by running `brew install bun`.

## How to install on Linux and WSL

Installing Bun on Linux is as easy as on macOS. Run `curl -fsSL https://bun.sh/install | bash`. That's it!

Linux users are recommended to make sure the unzip package is installed first. You should also be running the kernel in at least version 5.1, even if version 5.6 or higher is a better choice.

## How to install Bun on Windows

For now, unfortunately, Bun's package manager abilities are not available for Windows. But this shouldn't be a problem if you are running WSL.

There's currently an [experimental version](https://bun.sh/docs/installation#windows) for it, but it's not recommended to use it in production.

## Make some room to replace NPM, Yarn, or pnpm with Bun 

You don't need a specific package manager. You can use whichever one you want. Which is great news for Bun!

If you were using NPM or pnpm, remove their lock files because you won't need them anymore since Bun uses its own lock file called *bun.lockb* by default.

If you were using NPM:

```bash
rm package-lock.json
```

If you were using pnpm:

```bash
rm pnpm-lock.yaml
```

And if you were using Yarn:

```bash
rm yarn.lock
```

## Install your front-end dependencies using Bun's package management abilities

To install your dependencies using Bun, use `bun install`. So, how fast was it? I bet you didn't expect that!

Oh and by the way, in case of a problem, if you want to disable the cache, use `bun install --no-cache`.

For additional information and options, please refer to the [official documentation of the `bun install` command](https://bun.sh/docs/cli/install).

![bun install in action.](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/69/conversions/ybYunPr2RMZPLO3vFaMImsaecxEEnz-metaQ2xlYW5TaG90IDIwMjMtMDktMTEgYXQgMDkuMDAuMDJAMnguanBn--medium.jpg)

## Add a package using Bun

Adding a package using Bun can easily be done using the `bun add` command. You will certainly appreciate how incredibly fast it is as well.

Here's an example with 3 packages:

```bash
bun add tailwindcss autoprefixer postcss
```

For additional information and options, please refer to the [official documentation of the `bun add` command](https://bun.sh/docs/cli/install#bun-add).

![bun add in action.](https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/70/UndzC78D9Uclf8eMBlPr0yN2wbhXRy-metaQ2xlYW5TaG90IDIwMjMtMDktMTEgYXQgMDkuMDIuMTFAMnguanBn-.jpg)

## Remove a package using Bun

Removing a package using Bun can easily be done using the `bun remove` command. You will certainly appreciate how incredibly fast it is as well.

Let's use Axios as an example, since we can now use the native Fetch API:

```bash
bun remove axios
```

For additional information and options, please refer to the [official documentation of the `bun remove` command](https://bun.sh/docs/cli/install#bun-remove).

## Run your scripts using Bun

Bun should be able to be integrated into your existing workflow without any issues. Run the scripts defined in your *package.json* file just like before using `bun run`.

We can run our compilation process. For instance, I always use Vite:

```bash
bun run dev
```

For additional information and options, please refer to the [official documentation of the `bun run` command](https://bun.sh/docs/cli/run).

## Bun's video presentation

<iframe src="https://www.youtube.com/embed/BsnCpESUEqM?si=fvhqvQU9XY9_0dGT" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>