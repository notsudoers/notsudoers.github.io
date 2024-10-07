---
layout: post
title: My Dotfiles
date: 2024-10-06 09:49 +0700
description: "Customize Your Dotfiles for a Seamless Setup on New Servers!"
image:
  path: "../assets/img/posts/Dotfiles.png"
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: "source: Trust me bro"
categories:
  - Linux
  - Customization
  - Tutorial
tags:
  - shell
  - dotfiles
  - git
published: true
sitemap: false
pin: true
---

Hey everyone! Today, I want to share my personal dotfiles setup that I've crafted for a smooth and efficient workflow. If you’re diving into a new server or just looking to streamline your daily tasks, my dotfiles might just be what you need!

## What Are Dotfiles?

First off, dotfiles are configuration files for your system and applications. They’re usually hidden (with suffix dot ".") and can control everything from your shell preferences to editor settings. By customizing them, you can create a consistent and efficient environment tailored to your needs.

## Why Use My Dotfiles?

I’ve put together a collection of dotfiles that reflects my workflow, which includes:

- Terminal Customization: From bash to oh-my-posh, I’ve tweaked my prompt to be informative yet clean.
- Editor Settings: My preferred configurations for NeoVim using NvChad.
- System Preferences: A few personal touches that enhance my daily tasks.

## Let's get started

### Install necessary packages

#### For Arch Based

```sh
sudo pacman -Syy && \
sudo pacman -S --noconfirm base-devel git wget curl unzip htop npm bash-completion ripgrep python3-venv && \
git clone https://aur.archlinux.org/yay.git && \
cd yay && \
makepkg -si --noconfirm && \
cd
```

#### For Debian Based

```sh
sudo apt-get update && \
sudo apt-get install -y git wget curl unzip htop npm bash-completion ripgrep python3-venv
```

#### For RHEL Based

```sh
sudo dnf update -y && \
sudo dnf install -y epel-release && \
sudo dnf groupinstall -y "Development Tools" && \
sudo dnf install -y git wget curl tar unzip htop npm bash-completion ripgrep python3-venv
```

### Install neovim

```sh
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim-linux64.tar.gz && \
sudo tar -C /opt -xzf nvim-linux64.tar.gz
```

### Install oh-my-posh

```sh
sudo wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh && \
sudo chmod +x /usr/local/bin/oh-my-posh
```

### Configure Dotfiles

#### Clone this repository

```sh
git clone https://gitlab.com/notsudoers/my-dotfiles.git && cd my-dotfiles
```

#### Symlink all configuration to the home directory

```sh
ln -s $(pwd)/.gitconfig $HOME/.gitconfig
ln -s $(pwd)/.poshthemes ~/.poshthemes
ln -s $(pwd)/.inputrc ~/.inputrc
mkdir -p $HOME/{.config,.ssh}
ln -s $(pwd)/.config/* $HOME/.config/
ln -s $(pwd)/.ssh/config $HOME/.ssh/config
```

#### Add necessary value to the .bashrc

```sh
echo -e 'export PATH="$PATH:/opt/nvim-linux64/bin"' >> $HOME/.bashrc
echo -e 'eval "$(oh-my-posh init bash --config ~/.poshthemes/huvix.omp.json)" \nalias cl="clear"' >> $HOME/.bashrc
```

#### Load new configuration

```sh
source ~/.bashrc
```

#### Init neovim configuration first to installing all plugins stuff

```sh
nvim
```

Run `:Lazy sync` command to update to the latest plugins.

Run `:MasonInstallAll` command after lazy.nvim finishes downloading plugins.

Lastly change the value of git in `~/.gitconfig` to fit your settings.

## Final look

### Github repository

![Light mode only](../assets/img/posts/Dotfiles.png){: .light }
![Dark mode only](../assets/img/posts/Dotfiles.png){: .dark }

### Neovim

![Light mode only](../assets/img/posts/Nvim_light.png){: .light }
![Dark mode only](../assets/img/posts/Nvim_dark.png){: .dark }

## Conclusion

Dotfiles can really level up your productivity and help you maintain a consistent environment across devices. I hope you find my setup useful!

Feel free to explore, adapt, and share your own dotfiles as well. Let’s make our workflows as efficient as possible!
