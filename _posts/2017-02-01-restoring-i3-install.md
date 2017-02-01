---
layout: post
title: Setting up i3 on an existing install from dotfiles
date: 2017-02-01 23:35
permalink: i3-from-dotfiles
summary: I go over the steps needed to setup a fresh ubuntu install with i3 using my dotfiles.
categories: i3 linux
---

I've recently had to restore my i3-wm desktop from my home machine to a couple of new machines so I thought I'd note down all the steps for a quicker setup in the future.

- Install i3wm (Steps reproduced from [i3wm.org](https://i3wm.org/docs/repositories.html))
```bash
echo "deb http://debian.sur5r.net/i3/ $(lsb_release -c -s) universe" >> /etc/apt/sources.list
apt-get update
apt-get --allow-unauthenticated install sur5r-keyring
apt-get update
apt-get install i3
```

Remember to use apt-get and not apt otherwise the ubuntu will refuse to accept the unauthenticated package.

- Download any fonts that you need for your config. I use http://fontawesome.io/. Download the ttf and put it in a .fonts folder in the home folder.

- Get your dotfiles. I store mine on [github](https://github.com/chaitanyanettem/dotfiles). Move all contents of i3 folder in the dotfiles repo to ~/.config/i3/.

- Install any packages that might be needed now. I require lxappearance, arandr, synapse, rofi, dunst, compton.

- Install numix theme (sudo apt install numix-gtk-theme) and numix icons:
```bash
sudo apt-add-repository ppa:numix/ppa
sudo apt update
sudo apt install numix-icon-theme-circle
```


















































