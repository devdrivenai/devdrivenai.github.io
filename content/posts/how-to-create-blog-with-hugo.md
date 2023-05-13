---
title: "How I Created My Blog With Hugo"
date: 2023-05-12
draft: false
author: devdrivenai
description: How I built my Hugo blog (and how you can, too!)
categories: ['how-to', 'creation']
tags: ['hugo', 'blog']
---

## Why blogging (and why not?)

Hi there! To start with this post, I want to ask you that we do an exercise together. It consists of a question for you. If you are a developer (or even an aspiring one, like me) and you don't have your own blog, why haven't you done it yet? It will probably help you solidify what you know and distinguish what you understand from what you guess. Besides, there might always be someone who may find it useful.

Maybe you aren't doing it yet due to fear? I hear you! That's me, too. I plan writing about this, so definitely come back soon to see it published.

If you are procrastinating with it, what are you waiting for?

However, if you have your (different) reasons, I invite you to analyze if they're valid and also to think about the pros of actually having it, some of which I mentioned above.

If your reasons are valid, though, sorry for the question! Truth is I needed to ask that to myself, and I thought that may be you too. {{% spanclass emoji %}} :smiling_face: {{% /spanclass %}}

Now, then, let's talk about the how. About how I created my blog with Hugo. And also, in a future follow up to this post, we will chat about one of the simplest (and free!) ways to deploy this blog online and show it to friends, family and, equally important if not more, potential recruiters and employers.

First things first: let's talk about requirements:

## Requirements

If you want to do this with me, you will need to:
- have Hugo installed locally
- have Git installed locally
- have your own GitHub account (for deployment, but also to have your version control backed up)
- a terminal and/or code editor

With regards to the last item on this list, you could use different alternatives, whether do all within the terminal, use the editor's built-in terminal, or any combination thereof. My preferences are using the Git Bash (comes with Git for Windows) and/or WSL. And, as an editor, I use Visual Studio Code (I set the default built-in terminal to be Git Bash). But you can choose as you see fit for you. 

NOTE: Also, if you're on Windows, using the [Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701) might save you some headaches when needing multiple terminal windows. Obviously, you can customize this with any terminals you have available in your system and even your WSL.

## Choosing a theme

Trust me, this can be tough, but for a good reason. There is just so much variety and such good themes to choose from that it can become difficult to pick one! {{% spanclass emoji %}} :smiling_face: {{% /spanclass %}}

The good thing is that Hugo's website offers some [good guidance](https://themes.gohugo.io/), with previews, descriptions and filters.

However, if you don't find what you're looking for there, there's always the option of creating your own theme. But that would be an investment that you want to be sure is worth making.

In my case, though, right now I want to get started ASAP, not worrying too much about things that can be improved later on, since I want to push myself to deliver and put content out there in order to let go of the fear that has been holding me up for so long. 

I found the [PaperMod](https://adityatelange.github.io/hugo-PaperMod/) theme to be very appropriate for my specific use case, bringing (built-in) the features that were my main priorities, namely: light and dark mode, support for multilingual sites and, very important, a modern yet clean interface, that invites the reader to focus on the content, not to mention other perks it also has.

## Getting our way around Hugo commands

If you're somewhat like me, then you don't just like following instructions (or copy-paste them) without knowing first what you are doing and what you could do.

Fortunately, Hugo makes this very enjoyable in two ways: 1) the thorough [documentation](https://gohugo.io/documentation/) and 2) the `help` command and `--help` flag of their CLI. By the way, the documentation previously linked also includes a visual interface for the CLI commands and flags.

So, let's see our way around with the `help` command:
```shell
hugo help
```

One of the lines of the output states:
```
Available commands:
...
...
...
  new       Create new content for your site
```

Although this may seem to imply you already need to have a site going for this, you can actually also create one with the command: `hugo new site` *plus* the path or name for your project.

So, let's check the `--help` flag for that command:
```shell
hugo new --help
```
gives:
```shell
Available Commands:
  site        Create a new site (skeleton)
  theme       Create a new theme
```

NOTE: *As a rule of thumb, it's always a good idea to play around with the `--help` flag of a CLI until you get familiar with it. If you haven't tried it yet, this is a really good time to stop reading and get lost with it.* {{% spanclass emoji %}} :smiling_face: {{% /spanclass %}}

However, if you look at the flags, all of the flags available for both of these commands (`site` and `theme`) are listed.
The first one (`site`) is the one we're interested in right now:
```shell
$ hugo new site --help
Create a new site in the provided directory.
The new site will have the correct structure, but no content or theme yet.
Use `hugo new [contentPath]` to create new content.

Usage:
  hugo new site [path] [flags]

Flags:
      --clock string               set the clock used by Hugo, e.g. --clock 2021
-11-06T22:30:00.00+09:00
  -e, --environment string         build environment
      --force                      init inside non-empty directory
  -f, --format string              config file format (default "toml")
  -h, --help                       help for site
      --ignoreVendorPaths string   ignores any _vendor for module paths matching
 the given Glob pattern
  -s, --source string              filesystem path to read files relative from
      --themesDir string           filesystem path to themes directory

Global Flags:
      --config string      config file (default is hugo.yaml|json|toml)
      --configDir string   config dir (default "config")
      --debug              debug output
      --log                enable Logging
      --logFile string     log File path (if set, logging enabled automatically)
      --quiet              build in quiet mode
  -v, --verbose            verbose output
      --verboseLog         verbose logging
```

Well, there are fewer flags here, but they're still a lot.

## Getting our site going

Basically this output above tells us that we have to type `hugo new site` and then the `[path]` (by default the present working directory, so you just type the name of your project folder) and the `[flags]`, if any.

The path argument is required and what Hugo will do with it is creating that folder (or path) *inside* the folder you're currently in. And inside that new folder, it will add a number of directories and files that will be the basic structure of your Hugo blog.

The flags allow you to customize a lot of stuff to your liking and usecase. The one that we will use here is `-f` (or `--format` if you prefer), which requires to be followed by a string (`-f, --format string`). This string tells Hugo which of three possible formats you want the config* file to be: `.toml` (default), `.yaml` or `.json`. Since (as of now) I am the most familiar with json, let's specify it that way.

```shell
hugo new site mysite -f json
```

*TLDR TANGENT NOTE: *even though the `--config` flag mentions that the default config filename is `hugo.yaml|json|toml` (see output of `hugo new site --help` above), as of now (Hugo version 0.111.3) the config file created is still named `config.<extension_here>`. However, they are planning to change it to be `hugo.<extension_here>` by default, as mentioned [here](https://gohugo.io/getting-started/configuration/#hugotoml-vs-configtoml) in the docs and also in a comment in their source code, where they say they eventually will change the "config" to "hugo". If you manually change the filename from `config` to `hugo`, though, that will work too. Something to take into account.*

OK, let's get back on track now:

Let's pat ourselves on our own back! The new site is up! There hu-go! And, actually, if we take a look at the CLI output, Hugo gives us very helpful hints about what we still need to do:

```shell
Congratulations! Your new Hugo site is created in D:\\gh_clones\\mysite.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

## A first look at the structure of our site

Now, this will have created a folder with the name `mysite` within the current folder, with a `config.json` file that looks like this:

```json
{
   "baseURL": "http://example.org/",
   "languageCode": "en-us",
   "title": "My New Hugo Site"
}
```

...and the following folders:

`- archetypes/`

`- assets/`

`- content/`

`- data/`

`- layouts/`

`- public/`

`- static/`

`- themes/`

Except for `archetypes/`, they will all be empty. We will (probably?) talk further about them in the future, but for now that's unnecessary while we're getting used to the basics of Hugo. What matters now is that we get that first site going.

## Spinning up the server

Talking about that, can we already try to spin up the server? Will that work?

```shell
hugo help
```

```
Available commands:
...
...
...
  server      A high performance webserver
```

It is worth mentioning that, as discussed [here](https://discourse.gohugo.io/t/hugo-serve-vs-hugo-server/24872) and mentioned in their `--help` flag, `hugo serve` and `hugo server` will do exactly the same, as the former is just an alias of the latter.

So, guess what we are going to do next?

Exactly:

```shell
hugo serve --help
```

Well, as you can see in the output (if you are doing it with me) there are lots of flags available here, but we don't need any as of now. Let's just get it working with the defaults, without any tweaking.

```shell
hugo serve
```

Output:
```shell
WARN <date_here><time_here> found no layout file for "HTML" for kind "home": You should create a template file w
hich matches Hugo Layouts Lookup Rules for this combination.
WARN <date_here><time_here> found no layout file for "HTML" for kind "taxonomy": You should create a template fi
le which matches Hugo Layouts Lookup Rules for this combination.
```

That part of the output may look like something went wrong, especially if you follow the indication in this line:

```shell
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
```

When you open that on your browser, you'll get a boring, plain 404. What's wrong?

Remember the following line of the output to `hugo new site --help`? 
```shell
The new site will have the correct structure, but no content or theme yet.
```

Well, Hugo is looking for layout files (i.e.: files in the `layouts/` folder that explain Hugo how to "organize" your site's content). You could do this, of course, but this is where *themes* might help you get a quick start.

This is why we chose one earlier. I chose the [PaperMod](https://adityatelange.github.io/hugo-PaperMod/), remember? Which one did you choose?

OK then, let's bring our theme onboard. But wait, how?

## Including our chosen theme

Usually, theme creators will guide you a little on this, and our PaperMod theme [is no exception](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-installation/). Hugo also provides some basic guide [here](https://gohugo.io/getting-started/quick-start/).

As you can see, there are many different methods in which you can do this, but let's choose one of the simplest for now:
```shell
cd mysite # move inside your project's root directory
git init # initialize a repo in the root directory of your project
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
# obviously, the URL after 'add' above will point to the repo of your chosen theme
``` 

What you do here is you first initalize a repo with `git` and then you use the `submodule` git's [functionality](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to bring in the repo of the theme as a submodule inside the themes folder of your project with the name you specify (in my case, PaperMod, but yours should be your selected theme's name).

There's one more important step though: you have to tell Hugo to look for this theme in your project's settings (the config/hugo file mentioned earlier). Since I am using a `.json` file, this is how I'll do it:

*config.json*
```diff
...
+   "title": "mysitesfancyname",
-   "title": "My New Hugo Site",
+   "theme":"PaperMod"
...
```

Now, let's have a look at how the site looks, going to `http://localhost:1313/`

Well, regardless of which theme you choose, it will probably look a little... empty. That's because we haven't added any content yet.  

## Adding our actual content

Remember the output of `hugo new --help`? Part of it was:
```shell
Create a new content file and automatically set the date and title.
It will guess which kind of file to create based on the path provided.
```

The content, as we would expect, will go inside the `content/` folder. But then we decide what kind of content we want to add. If we want to add a blog post, we will do:

```shell
hugo new posts/hello-hugo.md
```

This will create a new `posts/` folder (if it wasn't created yet) inside `content/`, and a `hello-hugo.md` file inside the former, with the following content:

```
---
title: "Hello Hugo"
date: <date of the post here>
draft: true
---
```

That above is called ["front matter"](https://gohugo.io/content-management/front-matter/). We will talk about it in the future. For now, though, if we change `draft` to `false` (i.e.: not anymore a draft, now it's published!) or add the flag `-D`* to our `hugo serve` command (remain as draft, and yet be available anyway), we will now see our post in the browser.

*See:
```shell
-D, --buildDrafts                include content marked as draft
```
\
Equally, if we wanted, for example, an about page, we could have done:

```shell
hugo new about.md
```

Have a look for yourself. (Do take into consideration that the URL will no longer be under `posts/`.)

The way these are displayed will depend on the content of our `layouts/` folder (in our case, though, it's empty, and this is handled by the `layouts/` folder of our theme: `themes/PaperMod/layouts/`).

## What about deploying it?

The only thing remaining now is to write some markdown, so we have our pages and posts. Well, and we probably will also want to deploy this, so we can see it live, not just on our computer, but that will be on the next post.
