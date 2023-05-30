---
title: "How to Install Git"
date: 2023-05-30
draft: true
author: devdrivenai
description: About how to install and connect Git and GitHub on Windows and Ubuntu
categories: ['how-to', 'installation']
tags: ['git', 'github', 'windows', 'ubuntu', 'gh-cli']
---

## Why installing Git (and why not?)

Hi there! 

May be you already came to this post with an intention to install Git. If so, you can skip ahead to the next section (should you want to, you can help yourself with the table of contents above for faster navigation). 
If, however, you are wondering why you should install it, let me comment to you some of its interesting features:
- It's like having a `CTRL + Z` allowing us to retrace our steps without the need to remember exactly what lines we changed. This is why it's called a *version control* system.
- It allows us to teamwork in such a way that many people can change stuff in their machine, after which everything gets synchronized into a main "drawer" (called repository, or just *repo* for the friends). This is why it's called *distributed* version control system.
- It allows us to recover a file that we deleted (or someone else did) by accident or mistake.
- It allows us to see how a similar problem was solved without the need to be looking file by file, line by line (i.e.: just searching by *commit*, that is, whenever *that specific change* was made).
- It allows us to have an incredible amount of control over what's changed, and when it is changed, in your code.
- And much more.

Now that you're aware of that, I'd like to ask you, why not? If you think it's complex, honestly, it's true that (everything) is a little more daunting in the beginning, but if you integrate it on your workflow in every project you do, it will slowly grow on you, trust me.

*Assumptions made in this article*: I will assume you work on a Windows machine with (Ubuntu) WSL installed. However, if you are working in only one of them (Windows or Ubuntu), the pertinent instructions in this article should work for you.

## Installing Git on Windows

If we want to install Git on Windows, we will first need to head to [this URL](https://git-scm.com/download/win). Then, we can go ahead and just click on `Click here to download` at the top of the page.

Once we downloaded the installer, we can just click and follow the steps. However, at least in my case, I prefer to customize a few things. For example:
- I like adding a Git Bash profile to Windows Terminal (this is an option that I find really cool, since from Terminal, you can handle multiple tabs and different shells, like Git Bash, WSL, etc., at the same time, which you cannot -or at least, not as easily- do in Git Bash).
- In the step about the default editor, I tend to choose VSC (Visual Studio Code), since anyway I can still, should I want, open files with Vim from Git Bash.
- Also, I prefer to override the default branch name (for new repos) to `main` (we should see an option to do that).

There are many more customization options provided to us during the installation process. For me, these are my 'overrides', for now, and then I stick to the default in the rest of them. But do take into account, you don't need to choose the same. You could choose different options that suit your workflow. Also, do notice we can still [change anything](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) in our git configuration later on, from the `.gitconfig` file that should be located in the `Git/etc/` directory, within our installation path (default being `C:/Program Files/`, so for example `C:/Program Files/Git/etc/.gitconfig`) or in the `config` file inside the `.git` folder of a specific repo (if we want this config to apply exclusively to this repo in particular).

## Installing Git on Linux (Ubuntu)

If you are on Ubuntu, odds are you already have Git installed. Although it will do no harm to ensure.

So, let's first check if we already have Git installed. Well, actually, let's see if our sources* ([but, wait, what are these sources?](https://www.cyberciti.biz/faq/what-does-sudo-apt-get-update-command-do-on-ubuntu-debian/)) are up-to-date:

> *TLDR NOTE: Making sure that the remote repos that provide us our software have the latest version locally.

```shell
sudo apt update
```
(we'll need to provide our ubuntu user's password, as sudo requires admin privileges)

... and if anything needs updating, let's do so:

```shell
sudo apt upgrade
```

We will be required to type a `y` to agree to do the modifications, and then our packages will be updated. (Or just `sudo apt upgrade -y` in one step.)

Now it's time to check if we have git:

```shell
git --version
```

Normally, it will be installed, in which case it will just show the version of git, but if the output shows a message like 'git: command not found', then we will have to install it.

No worries, that's easy enough:

```shell
sudo apt install git
```
> *NOTE: We could also use `apt-get` instead of `apt`, [but the latter deletes previous software versions and is more modern](https://aws.amazon.com/compare/the-difference-between-apt-and-apt-get/), among other perks.

In my case, here I receive a message stating: `git is already the newest version`, but you should be now allowed to install it, prompting for your confirmation.

Once finished, to make sure everything went alright, we just have to type:

```shell
git --version
```

This should now show git's version.

And that's it. We already have git installed. Except now we will have to define its configuration.

## Creating a GitHub account (Windows and Ubuntu)

Creating a [GitHub](https://github.com) account should be a very straightforward thing to do, aided by the wonderful experience that GitHub offers on signup. I am not going to do a spoiler here, so you can experience this by yourself. I will just tell you it's one of the best signups I have seen in my life.

However, one thing we may want to take into account is that later, when we push our commits to GitHub, our email address would be publicly revealed. If we don't want this to happen, something we can set up is a *"noreply"* email address. This is a very simple process, though, and it may even be enabled by default, but if you are interested and you'd want to make sure, this is how we can do it:

Once we logged in on GitHub in our browser, we head towards the small arrow by the side of our user's profile picture, in the top right corner. We then unfold it and select `Settings`. Now, on the left hand side of our screen, we should see different sections of settings, among these, we should find the `Access` section, and inside it, the `Emails` option. Now, here we can decide if we want to have the `Keep my email addresses private` box checked. If so, this will work immediately for all web-based operations (i.e.: any operation we do in the browser). However, we should take into consideration that, below this box, GitHub warns us that we will also have to associate this *noreply* email in our *local* Git app, for it to also work with local Git operations (commits, pushes, etc.). In order to do so, we will find the *noreply* email address in the note under this checked box, as well as in the note under "Primary email address".

It is also possible to check the next box, `Block command line pushes that expose my email`, if we want to avoid that any command, by accident or in whichever way, ever exposes our email address(es).

So, OK, we now have Git and GitHub, but how do they know about each other? Through the `gitconfig/config` file we mentioned earlier. Let's chat about this.

## Connecting our local Git with our GitHub account (Windows)

Admittedly, there are different ways to do this. The one we are going to use is through HTTPS, but be aware you could also use [SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh), should this work better for your specific use case.

The first thing we want to do is add our email (whether our actual email or the *noreply* one, see above) to git's configuration. Whereas we could just open the pertinent file with Vim, Nano or even VSC, and editing it manually according to the changes below, there's a more convenient way, through Git's CLI:

```shell
git config --global user.email <your_email_address_here>
```

The setter is implicit when we add our email address, so the getter is just the same command, but without adding any email address. That is, if we want to check it was properly set, we could *get* the value of the config, doing almost the same, but without the email address:

```shell
git config --global user.email
```

And the output should be the email we've assigned.

> Word of caution: *If, for some reason, we want to use an email specific to this repo (let's say personal GitHub vs the one at work, for example), then we won't use the `--global` flag. In this way, the email entered will be stored inside the repo's `.git/` folder, not in your global git config file. Take into consideration that, if we do this, then on every new local repo, when we attempt to do our first commit, we will be asked to add an `user.email` config*.

Well, we can now start tracking our work with `git add`, `git commit`, `git push`, etc. Wait! I created a local repo and already made some commits, but now `git push` is complaining! Yes, that's because we just created a local repo. If we want to actually connect it with GitHub, we will need the repo on Github, too.

Here, also, we have many options, we could create the repo on GitHub and then follow the instructions there, we could follow the prompt on Git when we type `git push` in our CLI, or we could also use `gh`, the GitHub CLI. Which one would you choose? Just in case you're not sure, let's run through them all here. (Disclaimer: not *all* of them actually, because there are just so many ways. Creating the repo first on GitHub and then cloning it locally, for example, won't be mentioned here.)

### 1) Creating repo on GitHub and following the instructions

In the GitHub page, let's head up to the top right corner and we should see a `+` sign. Let's press it and it will give us some options, the one that matters to us is `New Repository`, so let's click on it. In the next screen, we just have to type the repo name under `Repository name` and decide whether this project will be public or private. The other options do not concern us for now. 

Then, let's press `Create repository`. Now, we will be faced with some different options. 

- We could choose to `Set up in Desktop` (yes, they even offer a GUI! You can download it [here](https://desktop.github.com/)) and install it on our system.
- We could choose to do this through HTTPS or SSH (as mentioned above, we are just going to go with the former here).
- They also offer us instructions on how to create a brand new local repo from the command line and push it to this one we've just created on GitHub (`…or create a new repository on the command line`).
- Finally, the one that concerns us now is under `...or push an existing repository from the command line`.

This option shows us on screen three CLI commands that we should enter on our local Git/Bash/Terminal, that basically do this, line by line:
1. Previous step: it may or may not be obvious, but we should first position ourselves in the root directory of the local repo with `cd`:
```shell
cd <root_dir_of_repo>
```
2. adding the `remote` (this GitHub repo) to our local repo (the folder in our system):
```shell
git add remote origin <repo_url>.git
```
3. changing the name of the main branch to `main` (this should not be necessary if we did it when we installed Git, see above):
```shell
git branch -M main
```
4. push our code to the repo (and [set the upstream](https://git-scm.com/docs/git-branch/2.13.7#Documentation/git-branch.txt--ultupstreamgt) with `-u`, so that the next time, you can just type `git push`):
```shell
git push -u origin main
```

Now we should be prompted to enter our GitHub password, and if we are running Git for Windows 2.29 or later (comes with the "newer" Git Credential Manager and supports OAuth), this should now be stored on our system. We shouldn't need to input it again. That's it! They're now connected!

> NOTE: If you happen to be on Windows and your credentials don't work, go [here](https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git) and look for the peach-colored boxes, towards the bottom of the page, for some orientation on how you can fix that.

From now on, we can just `git push` after committing and everything should work alright. 

### 2) Typing `git push` and following the prompts

Well, this one is actually not going to work, since at the point we do the `git push`, it will tell us that the (remote) repository is not found. However, if we followed the previous instructions in the Git CLI, it means the remote was already created (try `git remote -v` to see it), so once we create the repo with the corresponding URL, we should just push and we're good to go.

But then again, why did we include this method in this list? Well, because if you're git-pushing for the first time and you need to enter credentials but also the repo doesn't exist, etc., in a certain set of circumstances, you could feel a little lost.

So it's good to know that git is guiding us with the prompt mentioned above, which tells us this:

```shell
$ git push
fatal: No configured push destination.
Either specify the URL from the command-line or configure a remote repository using

    git remote add <name> <url>

and then push using the remote name

    git push <name>
```

It is very likely that here, we will be prompted for the password, but when we click to enter the password, this may open a blank browser tab or not open anything at all, since the URL of the repo does not exist yet.

The message should be something like this:
```shell
$ git push -u origin main
info: please complete authentication in your browser...
remote: Repository not found.
fatal: repository '<repo_URL_here>' not found
```

So now, as said above, once we actually created the online repo, if we try, once again, pushing, the password prompt should pop up again and, this time, it should work, because "it knows where it points to" online.

### 3) Install GitHub CLI and use it for this

If you are interested in this option, you want to go [here](https://cli.github.com/) to download the GitHub CLI tool.

Now we should follow the prompts and, once finished, open a Git Bash window (or the shell we use) and type `gh` (if we had Git Bash or Windows Terminal open, we should first close them and then reopen, otherwise `gh` won't still work). This command should give us a glance of the commands available. If it doesn't, it's likely something went wrong with the installation, so we should try it again.

As we can see in the output, any repo related stuff will fall under the `gh repo` umbrella, so let's see what we have:

```shell
gh repo --help
```

Although here we will see a vast number of options, let's zone in towards what concerns us, creating a repo, right?

```shell
gh repo create --help
```

And what you will see now is hugely helpful. On a GitHub level. Do have a good read and choose your path forward here. My favorite one is the interactive way.

So I will do:

```shell
gh repo create
```

...and then pick our options at each step. 

> NOTE: we should take into account that we may need to open Git Bash from Windows Terminal (or reinstall Git for Windows and "Enable experimental support for pseudo consoles" during the installation process, but I think the other option is a little bit less dramatic, right?) to make use of gh CLI's benefits.

So, we will have to choose the repo's name, visibility, and other options, as well as if we want to clone it locally. At the end of this process of just a few seconds, we will have a new folder created for our repo with git initialized, the remote properly set and so on. Now, we will just have to add our email config (if it's not globally set) and authenticate, like we did in the other options.

How cool is that?

## Connecting our local Git with our GitHub account (Ubuntu)

Once again, there are different ways to do this. And I have made some choices and assumptions, which may or may not be adequate for your case. I assumed that we're working on Windows/WSL combo. I have chosen to use HTTPS, not SSH. I have not chosen to use the GitHub token, but the `gh` CLI + `google-chrome` browser instead. Do take into account some of the other choices might adapt better to your specific case. In any case, getting familiar with this method should not hurt.

### Installing `gh` CLI

Installation instructions for the `gh` CLI are provided [here](https://github.com/cli/cli/blob/trunk/docs/install_linux.md). However, if you are a little curious like me, you would probably want to know what we are actually doing here, right?

So let's go step by step:

1.
```shell
type -p curl >/dev/null || (sudo apt update && sudo apt install curl -y)
```
*TLDR: The line above is checking if we have `curl` installed, and if not, is installing it.*
> [*--verbose-reading mode alert*:
> 
>`type <app>` just tells you the path where an app is installed. For example: `type curl` would output `curl is /usr/bin/curl`. \
>
>The `-p` flag will only output the path section of the previous output (i.e.: `/usr/bin/curl`). 
>
>The `>` output operator sends the output somewhere (to a file, for example). 
> 
>And the `/dev/null` destination is sort of like a trash can, in the sense anything goes to it just disappears, it is like a digital black hole. {{% spanclass emoji %}} :smiling_face: {{% /spanclass %}}
> 
>So putting all of this together: find out the path of curl but I don't need it now, don't give it back to me...
> 
>So, here we query for a path, but what if we do it with an app that is not installed?
>```shell
>type microsoft-edge
>-bash: type: microsoft-edge: not found
>```
>It is not found or, simply put, that path *does not exist*.
>
>Then, we have ||, which basically means if the result of the previous command did not exist (i.e. if `curl` is not installed)... then `sudo apt install curl -y`, the -y flag making sure you don't have to confirm all the `y`es prompts.
> 
>In all honesty, though, I think we could have just done `curl` here and, if not found, then install it. However, this codeblock is meant to be executed all at once (hence the `\` at the end of each line) and, thus, can't be interrupted. That's why these instructions are this way.
> 
> *end --verbose-reading mode*]

2.
```shell
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
```
Essentially, what we do here is download the file at the URL provided (hence `curl` -> Client URL) and duplicate it (or copy it) into the path provided after the `sudo` command (sudo for permissions, obviously).

3.
```shell
sudo chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg
```
Give 'reading' permissions on that file to 'group' and 'others'. So, `chmod` would be 'change mode' (i.e.: change permissions of a file) and then 'go' ('group' and 'others'), '+' (add), and 'r' (read).

4.
```shell
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
```
This one is a little more involved, but the TLDR is this: remember when we do `sudo apt update` and `upgrade`? Well, the system knows what to check because of the system's list of available repos. Now, with this command we are adding the one specified, so that we can now install (and, eventually, update) the `gh` CLI. Actually, after running this command, feel free to open `sources.list.d` and `github-cli.list` (under the path specified in the command) with vim or nano and you'll see. Since we used `echo`, which tends to display output, we end it with the output operator (`>`) and `/dev/null`, which should sound familiar (see above).

5.
Then,
```shell
sudo apt update
```
to update the sources, and:
```shell
sudo apt install gh -y
```
... to install `gh` CLI and automatically confirm all prompts with `y`.

By now, if we type `gh`, we should receive a thorough welcome output with a lot of options of what we can do (i.e.: commands, flags, etc.).

### Installing Chrome

Yes, even if you're using WSL, you can install Chrome on Ubuntu. "But... you mean like with GUI and all?" I hear you ask. Yup!

The instructions for doing so are [here](https://learn.microsoft.com/en-us/windows/wsl/tutorials/gui-apps#install-google-chrome-for-linux). So, let's go through them:

1.
```shell
cd /tmp
```
Just head to the `tmp` folder, the place to store files that are going to be *temporarily* necessary. 

2.
```shell
sudo wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
In this case, instead of using `curl` (which we could have perfectly done), the instruction shows us the way to download the file in the path specified using `wget` (normally preinstalled with Ubuntu).

3.
```shell
sudo dpkg -i google-chrome-stable_current_amd64.deb
```
Notice we didn't have to update our sources or something like that. That is because we will use this command above instead of `apt install`. Additionally, the `dpkg` command only installs the package we specify, whereas `sudo apt install` would also install the dependencies. So, in essence, what we do with this command is install the package via the file we just downloaded. Why? Because we are not provided an Ubuntu repo from which to download, but a .deb file. However, you will notice the following message in the output of this command:
```shell
dpkg: dependency problems prevent configuration of google-chrome-stable:
```
...followed by a huge list of missing dependencies.

4.
```shell
sudo apt install --fix-broken -y
```
That's why now, we have to make sure any dependencies issues are solved (this one may take a while, since there's a bunch of deps).

5.
```shell
sudo dpkg -i google-chrome-stable_current_amd64.deb
```
By now running this command again, we should be out of the woods, with the `google-chrome` package installed.

If you are ready to be gratefully surprised, just type `google-chrome` and look at that Ubuntu GUI Chrome window open in front of your eyes. How cool was that?

### Authenticating Github through `gh` CLI and Chrome

It's unbelievable how simple they've made this one. We just have to type:
```shell
gh auth login
```
...and we will receive an interactive prompt to ask us if we want to log in on GitHub.com or Enterprise, if we want to use HTTPS or SSH, if we want to use a GitHub access token or simply the browser, and then, if we chose the HTTPS -> browser option, we will receive a code in the CLI and be prompted to press `Enter` to open our browser.

Once we do that, the browser we installed (Chrome, in our case) will open up with a GitHub window asking us to log in and paste (or enter) the code received, and then press 'Authorize GitHub'.

Once we do those, we'll have our `gh` CLI authenticated. So now we could clone a repo or create our own using it. We mentioned how to create a new repo in the section "[3) Install GitHub CLI and use it for this](#3-install-github-cli-and-use-it-for-this)", so let's now clone an existing repo.

Well, this is very simple, and it is even indicated to us in the repo's page on GitHub. If we go to our repo on GitHub, we'll find a green 'Code' button with an arrow at the top right corner. Should we click on it, it will offer us different options of how to clone the repo either locally or on 'Codespaces'. First one is the one that concerns us. Notice there are three ways indicated to us here: HTTPS, SSH and (our chosen option) GitHub CLI. The last one shows the command necessary (and we can even copy it right there): 
```shell
gh repo clone <gh_user/repos_name>
```
We should take into account we don't need to suffix this with `.git`, like in the HTTPS method.

However, you will notice that all options are shown there, even the [GitHub Desktop](https://desktop.github.com/), if you are a bit more of a graphical user.

Well, there's a lot more about how to use them side-by-side (Win-WSL) and this article is getting rather lengthy, but do have a glance at [this page](https://code.visualstudio.com/docs/remote/troubleshooting#_resolving-git-line-ending-issues-in-wsl-resulting-in-many-modified-files) (and other similar resources, if you want, of course) to, by all means, do further configs so everything adapts to your workflow.

## Conclusion

In the end, this process will certainly be tougher the first time around, but after we do it a few times, it should become second nature. And, in exchange, it will offer us so many advantages! Like being able to trace back after we made a mistake, backing up our repos online, so if our computer collapses, we don't lose anything, collaborate with others on the same project, and there's more! This was just to name a few.

Overall, using Git and GitHub is a decision we won't regret.
