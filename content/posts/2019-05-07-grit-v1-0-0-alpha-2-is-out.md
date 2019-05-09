---
date: 2019-05-07T14:30:59.594Z
title: "Announcing Grit: a Markdown editor for blogging with a static site generator"
---

Last year I decided to write more. I thought I'd try a hosted solution because I wanted to concentrate on the writing and not on the fiddling with the site.

[Micro.blog](http://micro.blog) was the most attractive solution to me but after using it for a while I realized that, as a developer, I am not capable of leaving the building of my blog to somebody else. There were too many things I wanted to tweak/change, bugs I couldn't live with etc. 

So I ended up sticking with my [Hugo](http://gohugo.io) solution.

Unfortunately there are many little annoyances when blogging with a static site generator, due to the fact that your posts are a bunch of Markdown files in a folder with a specific file name and some frontmatter boilerplate in them.

Creating a blog post was always tedious. Too many little fiddly things to do before you could just start to write. 

In order to remedy this I created a [blog-cli](https://github.com/kahlil/blog-cli) that just schaffolds new blog posts for me. It works fine but I really wanted an editor that can do that for me. 

That's why I built [Grit](https://github.com/kahlil/grit). It's a little Electron app that let's you manage a folder full of Markdown posts and edit them as well.

It allows you to store the path to your Markdown files, filter through the files, create a new file, edit the file and publish via Git. 

I used [Preact](https://preactjs.com/) and [htm](https://github.com/developit/htm) to write it because I was too lazy to set up a build step and I love writing code the browser can directly interpret. For the file editing part in Grit I am using [CodeMirror](https://codemirror.net/) which is a hell of a product, wow. 

If you use Hugo, Jekyll, Gatsby or whatever other static site generator to build your blog and are looking for a little convenience there, give it a spin! See the current feature list [on GitHub](https://github.com/kahlil/grit). 

It's an alpha version so there be dragons. But I am planning a bunch of improvements like: drag and drop images, configurable frontmatter and some enhancements around file-creation.

If you want, let me know what you think [on Twitter](https://twitter.com/kahliltweets).




