---
title: 'Committable & Team-Wide Enforceable Git Hooks With Husky'
date: '2017-08-16'
---

Git hooks are pretty much the shit. They allow you to run any script at different points during the life cycle of a commit.

> The pre-commit hook for example allows you to execute a script before the commit command does anything. That can be useful if you want to lint or test your code before it is committed.

The thing that is annoying about them is that the hook script files lie in your .git folder which is your local Git database. This means they don't get committed. And every member in your team has to copy the Git hook files manually into the right location into a folder that is hidden in your directory by default 😐.

So what to do when you want to keep your Git hook scripts in your repository and you want your whole team to reliably execute the exact same Git hooks?

There is an npm package for that. It’s called Husky. I ❤️ Husky!

Husky allows you to commit the script for your Git hook in your repository and makes sure that they get reliably get executed for anybody who checks out and installs your project.

How does this work?
When you install Husky with npm or yarn it executes a postinstall script that copies a bash script for every single Git hook into the .git/hooks folder. When the Git hooks are called these scripts check for an npm script of the same name as the Git hook and execute it if it exists.

This means after Husky is installed you can add npm scripts to your package.json like so:

```js
"scripts": {
  "precommit": "eslint"
}
```
Husky will make sure to execute this script when the pre-commit hook is called.
This means you can run any script for any Git hook you want. You just have to make sure that an npm script with the corresponding Git hook name exists (just without the dashes).

This makes Git hooks easy to manage and enforceable for a whole team working on one project.
It also makes the scripts easy to test because you can just run them with npm like: npm run precommit.
An important little detail that I discovered when using Husky at work is that the Husky postinstall script is not executed when the project is installed by a CI system. This is great because typically your CI merges branches into master and you typically don’t want the Git hooks to run in that case.

I was curious to see how Husky knows that it is being installed on a CI so I checked out the code. It uses an npm packages called is-ci which in turn uses an npm package called ci-info which basically just checks for a bunch of known names / constants / environment variables of various CI systems. So Husky does not execute postinstall if any of these exists.

Very cool, I had already started thinking about how to exclude Husky on CI installs 😄.
So long story short, Husky is a great way to manage Git hook scripts in your project.
