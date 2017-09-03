---
layout: post
title: "Windows 10 for MacOS/Linux development environment"
date: 2017-09-02 19:34:16 -0700
description: My personal notes and setup for Linux development using Windows 10.
published: true
---

Lately I've been tracking updates to Windows' Linux Subsystem, which is a surprising new chapter for Windows developers. I can now do Node/Ruby/web development the way I'm used to doing it in MacOS and Linux with Windows!

The technical nitty-gritty is that Microsoft's developers have been working on making Windows interpret all of Linux's [POSIX](https://en.wikipedia.org/wiki/POSIX) system calls. These are basically APIs that date back to the 1970's and represent all of the low-level hardware interactions that Unix-based OSs use. Everything from reading and writing to files to networking to cpu threading is covered by POSIX.

It's been a work in progress for the past couple years, but with the Fall Creators Update it's finally gotten to a point where you can download a Ubuntu Windows Store App.

![Windows Store on the Ubuntu "app"]({{ site.url }}/assets/img/2017-09-02-ubuntu-windows-store.jpg "Ubuntu, a Windows Store app?")

Beware, it takes some amount of tuning to make it work though. First of all, using the shiny Ubuntu app from the Store requires you get on the Fall Creators Update--doing that now instead of waiting until late October means signing up with the Windows Insider Program and using potentially buggy versions of Windows.

That being said, I haven't run into any serious issues yet on my laptop, but results may vary.

### Working with files and folders

So now you can open Ubuntu and see a blank terminal.
```
username@computer:~$ _

```
Welcome to Bash!

But this prompt can be misleading, especially if you're always used to starting in your Home directory in MacOS and Linux environments. Although this is your Ubuntu Home directory (/home/ubuntu-username) this is totally separate from your Windows User directory (C:\Users\windows-username). Any files and changes you make in the Ubuntu Home directory will only really be accessible by the Ubuntu Bash prompt, and files in this directory are difficult to manipulate with Windows programs.

You can get to your Windows files by using `cd /mnt/c` which will get you to your C:\ drive and if you have other partitions or drive letters, they should all be under /mnt.

To make use of your actual files, you can make [symlinks](https://en.wikipedia.org/wiki/Symbolic_link#POSIX_and_Unix-like_operating_systems) in your Ubuntu Home directory in order to work with your files in your Windows User folder. For this example, let's say you have a 'projects' folder in your Documents folder full of coding projects that you want to use in Ubuntu Bash:

```
ln -s '/mnt/c/Users/<windows username>/Documents/projects' /home/<ubuntu username>/projects
```

Using `ln -s` you can set up various symlinks in your Ubuntu Home directory and now you can quickly navigate to all of your important files using Bash, without having to go to /mnt/c etc. every time you start Bash.

### Setting up your environment

So now you can access your projects, how do you set up your development environments? Actually, you do it the same way you would on Ubuntu--it just works!

For instance, to set up Node, follow their [Ubuntu instructions](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions):

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

On top of that, you can easily open your files using Windows programs in Bash. If they have a path in Windows command prompt, it will carry over to Bash, so you can do:

`atom index.html`

And your file will open in Atom editor just like it does on the command prompt.

### A better terminal

If you're finding the vanilla Windows command window lacking, you can substitute it for any other Windows console client. Just open your preferred program and type in `bash` and it will switch to Ubuntu bash!

![A screenshot of Hyper running Bash]({{site.url}}/assets/img/2017-09-02-hyper-bash.png "Hyper is a much prettier way to use Bash in Windows")

My own preference is [Hyper](https://hyper.is/), and Linux Bash just works out of the box and can be configured to start there by editing this part of the config file:

`shell: 'bash.exe',`

You can find good Hyper themes and plugins here: https://github.com/bnb/awesome-hyper and add them using the config file.

With these steps done, you are now ready to take your MacOS/Linux development workflow to Windows!
