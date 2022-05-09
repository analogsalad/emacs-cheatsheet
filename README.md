# Emacs Tips & Keymaps
**Table of Contents**
1. [Shortcuts](#shortcuts)
   + [Evil Navigation](#evil-navigation)
   + [General](#general)
       + [Search And Destory](#search-and-destroy)
       + [Windows](#windows)
       + [Buffers](#buffers)
   + [Projects (Projectile)](#projects-projectile)
   + [Terminal (eterm)](#terminal-eterm)
   + [File Explorer (treemacs)](#file-explorer)
   + [Sly](#sly)
2. [Doom Configuration](#doom-configuration)
   + [Config Location](#config-location)
   + [Doom Commands](#doom-commands)
3. [Resources](#resources)

## Shortcuts

### Help

| Help                                 | Shortcut    | Notes |
|--------------------------------------|-------------|-------|
| Look up following key sequence       | `spc h k`   |       |
| Search keybinds available in context | `spc h b b` |       |


### Evil Navigation

| evil                                 | Shortcut    | Number modifier |
|--------------------------------------|-------------|-----------------|
| Jump to start of next word           | `w`         | `3w`            |
| Jump to end of current word          | `e`         | `5e`            |
| Jump to beginning of current word    | `b`         | `8b`            |
| Find and move to next occurrence     | `f`         |                 |
| Find and move to previous occurrence | `F`         |                 |
| Find the next character `j`          | `fj`        |                 |
| Find the previous character `j`      | `Fj`        |                 |
| Toggle visual block mode             | `ctrl v`    |                 |
| Insert in visual block mode          | `I` + `esc` |                 |


### General

| General                   | Shortcut           | Notes |
|---------------------------|--------------------|-------|
| Find invoked command      | `C-h ?`            |       |
| Find file                 | `spc f f`          |       |
| Find recent file          | `spc f r`          |       |
| Go to definition          | `spc c d` or `gD`  |       |
| Go to references          | `spc c D`  or `gD` |       |
| Look up documentation     | `spc c k` or `K`   |       |
| Compile                   | `spc c c`          |       |
| Evaluate Code             | `gr` or `gR`       |       |


##### Search and Destroy

| Search and Destroy                     | Shortcut    | Notes |
|----------------------------------------|-------------|-------|
| Search across project                  | `spc s p`   |       |
| Search another project                 | `spc s S-p` |       |
| Search in directory (recursive)        | `spc s d`   |       |
| Search in another directory(recursive) | `spc s S-d` |       |

After you search, hit `C-c C-e` to activate `wgrep-mode`. Edit the results
and hit `Z Z` to save your changes.


##### Windows

| Windows                     | Shortcut     | Notes |
|-----------------------------|--------------|-------|
| Split vertically            | `spc w v`    |       |
| Split horizontally          | `spc w s`    |       |
| Cycle Windows               | `spc w w`    |       |
| Jump to window in direction | `spc w hjkl` |       |
| Move window in direction    | `spc w HJKL` |       |
| Close window                | `spc w d`    |       |
| Increase/Decrease Height    | `spc w +-`   |       |
| Increase/Decrease Width     | `spc w ><`   |       |

##### Buffers

| Buffers                   | Shortcut           | Notes |
|---------------------------|--------------------|-------|
| Create new buffer         | `spc b N`          |       |
| Save buffer               | `spc b s`          |       |
| Kill buffer               | `spc k b`          |       |
| Previous buffer           | `spc b [`          |       |
| Next buffer               | `spc b ]`          |       |
| Switch buffers in project | `spc b b`          |       |
| Switch buffers globally   | `spc b B`          |       |

### Projects (projectile)

| projectile           | Shortcut               | Notes |
|----------------------|------------------------|------|
| Browse projects      | `spc p p`              |      |
| Add new project      | `spc p a`              |      |
| Remove known project | `spc p d`              |      |
| Find file in project | `spc spc` or `spc p f` |      |
| Save project files   | `spc p s`              |      |
| Compile project      | `spc p c`              |      |

**Notes:**

It's also possible to add the following to your `config.el`:

`(setq projectile-project-search-path '("~/dev/"))`

All projects in the the sub-directory will be indexed, and you will be able to navigate them, using `spc p p`.

### Workspaces

| workspaces                | Shortcut            | Notes |
|---------------------------|---------------------|-------|
| Open a new workspace      | `spc tab n`         |       |
| Switch between workspaces | `alt + 1` `alt + n` |       |
| Save workspace            | `spc tab s`         |       |
| Load workspace            | `spc tab l`         |       |
| Close workspace           | `spc tab c`         |       |

### Terminal (term)

| eterm           | Shortcut  | Notes |
|-----------------|-----------|------|
| Open term popup | `spc o t` |      |

### File Explorer (treemacs)

| treemacs                 | Shortcut  | Notes |
|--------------------------|-----------|-------|
| Open project tree        | `spc o p` |       |
| Close project tree       | `q`       |       |
| Explore files in dir     | `spc .`   |       |
| Create file              | `c f`     |       |
| Create directory         | `c d`     |       |
| Rename file/dir          | `R`       |       |
| Delete file/dir          | `d`       |       |
| Copy file/dir            | `y f`     |       |
| Move file/dir            | `m`       |       |
| Refresh                  | `g r`     |       |
| Open file (no-splitting) | `o o`     |       |
| Open file horizontally   | `o v`     |       |
| Open file vertically     | `o s`     |       |
| Open file externally     | `o x`     |       |


### Sly (Working with Lisp REPL)

| sly                   | Shortcut    | Notes |
|-----------------------|-------------|-------|
| Auto-complete in REPL | `,`         |       |
| Create/Connect to Sly | `spc m '`   |       |
| Previous Command      | `C-n`       |       |
| Next Command          | `C-p`       |       |
| Compile to `fasl`     | `spc m c c` |       |
| Compile function      | `spc m c f` |       |
| Compile region        | `spc m c r` |       |
| Compile and load file | `spc m c C` |       |
| Compile and load file | `C-c C-c`   |       |
| Load file             | `spc m c l` |       |


## Doom Configuration

### Config Location

`${HOME}/.doom.d/config.el`   - _Custom config, this is your private config._

`${HOME}/.doom.d/init.el`     - _Initializes modules at startup time._

`${HOME}/.doom.d/packages.el` - _Define the packages that you want to install._


You can use `spc f p` to peek into this directory.


### Doom Commands

Doom command line tool lives in `.emacs.d/bin/doom`, and it has some useful commands:

`doom install` - _Installs packages that you've defined in `packages.el`_

`doom update`  - _Updates packages._

`doom sync`    - _Synchronizes packages and configs._

`doom upgrade` - _Updates Doom itself._

`doom doctor`  - _Helps with diagnosing common issues with your config or environment._

## Resources

1. [Tecosaur Doom Emacs Config Book](https://tecosaur.github.io/emacs-config/config.html#)
2. [Doom Emacs Cheatsheet](https://gist.github.com/hjertnes/9e14416e8962ff5f03c6b9871945b165)
3. [Zaiste Programming - Emacs Doom Screencast Playlist](https://www.youtube.com/watch?v=rCMh7srOqvw&list=PLhXZp00uXBk4np17N39WvB80zgxlZfVwj)
4. [Emacs Doom for Newbies - Article](https://medium.com/urbint-engineering/emacs-doom-for-newbies-1f8038604e3b)
5. [Seorenn - Emacs Doom Screencast Playlist](https://www.youtube.com/watch?v=zVFqLNps-K0&list=PLPNohcoOBa5FT65hMZL6SkFmbyqFaLe3b)
6. [EmacsCast - Emacs Screencast Playlist](https://www.youtube.com/watch?v=7vC8al1ZZz8&list=PLIrdJT_FTtEZb6Mv_tF9L2AO9XXUNnTyj)

