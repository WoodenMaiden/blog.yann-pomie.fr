---
draft: true
---
Obsidian is a great note taking tool! From simple enhanced markdown to note linking I've been using this software for a little time now (even for this blog using [quartz](https://quartz.jzhao.xyz/)). However there is one small but frustrating issue: each Vault has it's own configuration and plugins, and I don't want to replicated changes across all my vaults.

A few weeks ago I saw a [video from the YouTube channel Dreams of Automation](https://www.youtube.com/watch?v=y6XCebnB9gs) in which he showed a way to use versioning on his `.config` files and sync them on GitHub. 

The backbone of his trick is the ``stow`` command, which we will us to have a single configuration directory to configure all vaults on our computer 

> [!NOTE]
> Apparently Obsidian has a directory for [global settings](https://help.obsidian.md/Files+and+folders/How+Obsidian+stores+data#Global+settings), However From what I've seen and experienced, this does not work

## GNU `stow`

When landing on the gnu web page we can see this introduction

>[!QUOTE]
>"GNU Stow is a symlink farm manager which takes distinct packages of software and/or data located in separate directories on the filesystem, and makes them appear to be installed in the same place."
>
>_\- The project's page_

It might not seems clear, but basically, `stow` will allow you to place files from many directories (aka "stow directories") into a single directory (aka "the target directory"). These new files are actually symbolic links targeting their source stow directories.

For instance I have applied the trick of Dreams of automation for both my `.config` files and my `.zshrc`, then in that case the stow directory is `~/dotfiles` and the target directory is `~`, here is how my target directory looks like: 

![[Pasted image 20240226181630.png]]

And here is my stow directory: 

![[Pasted image 20240226181919.png|center]]

As you can see files and directories such as `~/.zshrc` or even `.config/alacritty` are symbolic links targeting my `dotfiles` directory.

> [!NOTE]
> As you might notice the target directory also contains files and directories that are not stowed anywhere such as `~/.config/discord`

## Setting up 