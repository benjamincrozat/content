---
Image: https://github.com/damms005/devdb-vscode/raw/HEAD/resources/screenshots/light-dark-mode.png
Title: Auto-loading databases in VS Code using DevDb
Description: If you use VS Code and work with databases, DevDb is a nice database GUI client that loads your database using configuration from your workspace codebase and displays the data right inside the IDE!
Canonical: https://marketplace.visualstudio.com/items?itemName=damms005.devdb
Audio:
Published at: 2024-01-08
Modified at:
Categories: databases, laravel, tools
---

There is a high chance that if you use VS Code, you are using the integrated terminal rather than the system terminal/cli app. This is because we love and appreciate the advantages that such an integration brings, e.g.:

1. **Less context-switching**. There is less distraction especially when you want to really focus on the task at hand. The lesser you have to switch from one app to another, the better the DX (Developer Experience). Switching to-and-from apps is obviously not good when trying to focus on a database related coding/dev task.

2. **Contextual integration**. Another advantage is that VS Code is able to provide integrations related to the currently opened workspace. e.g. The `cwd` defaults to the project root, you can click on links to files from the terminal to open it in the IDE, etc.

The above are just a few of the advantages when VS Code provides integrations for tools.

Now, why can't we have the same experience when working with databases? Why do we have to configure our database credentials in our project (e.g. `.env` in Laravel) *and* also configure it in another database GUI desktop app? Why do we have to switch from VS Code to TablePlus/phpmyadmin/whatever-your-favourite-database-desktop-app-is? Ask no more, because you can now use [DevDb](https://marketplace.visualstudio.com/items?itemName=damms005.devdb)!

DevDb is a framework- and language-agnostic VS Code extension that auto-loads your database without the need for configuring database connection separately from what you already configured in your application code. It currently [supports SQL, MySQL, and Postgres databases](https://github.com/damms005/devdb-vscode/#supported-databases), with plans to support more databases in the future.

**DevDb features**
1. It auto-loads your database and shows your data right inside VS Code. In a Laravel project, this is done by processing some files like `config/database.php`, `docker-compose.yml`, and `.env`
2. If it cannot auto-load your database (yet 😉), you simply provide a [`.devdbrc` file](https://github.com/damms005/devdb-vscode/#2-config-based-database-loading) in the root of your application. This is why you can use it in any framework and any programming language
3. In any tool, framework, or programming language, you can open any table using the provided context menu feature. The example below is from a Node JS project:
![image](https://github.com/damms005/devdb-vscode/raw/main/resources/screenshots/context-menu-contribution.png)
4. It provides [Code Lens](https://code.visualstudio.com/blogs/2017/02/12/code-lens-roundup) in Laravel Eloquent models
![image](https://github.com/damms005/devdb-vscode/raw/main/resources/screenshots/laravel-code-lens.png)
5. It has a nice and intuitive interface, and makes navigation a bliss!
6. It has dark mode! I mean, why not? 😜
7. When you're not in a hurry and idle, it tells actual dad jokes:
![image](https://github.com/damms005/devdb-vscode/raw/main/resources/screenshots/devdb-dad-joke.png)
8. And what's more? It's Open Source! You can tinker with [the source code](https://github.com/damms005/devdb-vscode/) and PR anything you're missing.

You can start using DevDb right now. Check it out in [the VS Code marketplace](https://marketplace.visualstudio.com/items?itemName=damms005.devdb).