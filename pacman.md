---
type: article
title: pacman
description: Using Pacman on Arch Linux
tags:
  - pacman
  - arch
  - yay
lastmod: 2023-09-26
published: true
---

## what is pacman

Arch Linux package manager utility.

## flags

- `S` installing or updating programs / keeping them synced with remote repositories
- `R` remove programs
- `Q` searching locally for programs
-

## common commands

- Synchronize and update all packages:
  `sudo pacman -Syu`

- Install a new package:
  `sudo pacman -S package`

- Remove a package and its dependencies:
  `sudo pacman -Rs package`

- Search the database for packages containing a specific file:
  `pacman -F "file_name"`

- List installed packages and versions:
  `pacman -Q`

- List only the explicitly installed packages and versions:
  `pacman -Qe`

- List orphan packages (installed as dependencies but not actually required by any package):
  `pacman -Qtdq`

- Empty the entire pacman cache:
  `sudo pacman -Scc`

- List only the explicitly installed packages and versions through the AUR:
  `pacman -Qm`

## configure pacman

```sh
sudo vim /etc/pacman.conf
```

is use those configurations

```md
# Misc options
#UseSyslog
Color
ILoveCandy
#NoProgressBar
CheckSpace
#VerbosePkgLists
ParallelDownloads = 5
```

## aliases i use

```sh
alias pi='sudo pacman -S $1'
alias psearch='sudo pacman -Ss $1'
alias pr='sudo pacman -R $1'
alias prs='sudo pacman -Rs $1'
alias prns='sudo pacman -Rns $1'
alias pu='sudo pacman -Syu'
alias pl='sudo pacman -Qe'
alias pw='sudo pacman -Qi $1'        # info about a package
alias cleanup='prns $(pacman -Qtdq)' # remove orphaned packages
alias dop='sudo pacman -Sc' # delete old packages
```

## update the mirror list

I just use this command after i install the rate-mirrors package

```sh
rate-mirrors --allow-root --protocol https arch | sudo tee /etc/pacman.d/mirrorlist
```

## advices

just use an AUR helper like Yay

## resources

- [Using Pacman on Arch Linux: Everything you need to know](https://youtu.be/-dEuXTMzRKs?si=R5QRVKceR-C-USg4)
