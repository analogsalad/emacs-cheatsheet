# Emacs Tips & Cheatsheet

This document is a collection of my notes on everything Emacs and Doom. Keep in mind that most of the material is optimized for my preferences and as a result, highly opinionated.

**Table of Contents**
1. [Building Emacs](#building-emacs)
2. [Installing Doom](#installing-doom)
   + [Doom Configuration](#doom-configuration)
   + [Doom Commands](#doom-commands)
3. [Shortcuts](#shortcuts)
   + [Evil Navigation](#evil-navigation)
   + [General](#general)
     + [Search And Destory](#search-and-destroy)
     + [Windows](#windows)
     + [Buffers](#buffers)
   + [Projects (Projectile)](#projects-projectile)
   + [Terminal (eterm)](#terminal-eterm)
   + [File Explorer (treemacs)](#file-explorer)
   + [Sly](#sly)
   + [Org-Mode](#org-mode)
     + [Headlines](#headlines)
     + [Lists](#lists)
     + [Links](#links)
     + [Content](#content)
     + [TODOS](#todos)
     + [Tags](#tags)
     + [Exporting](#exporting)
4. [External Resources](#resources)

## Building Emacs

**Step 1. Download Emacs**

> You can check the latest version here: https://ftp.gnu.org/gnu/emacs/

`wget -P ~/tmp https://ftp.gnu.org/gnu/emacs/emacs-27.2.tar.gz`

**Step 2. Unzip**

`tar -xzvf emacs-27.2.tar.gz && rm emacs-27.2.tar.gz`

**Step 3. Install Dependencies**

```bash
sudo apt-get install build-essential automake \
    libgnutls28-dev libgtk-3-dev libwebkit2gtk-4.0-dev \
    libxpm-dev libc6-dev xaw3dg-dev zlib1g-dev libx11-dev libjansson-dev \
    librsvg2-dev libjpeg62-turbo libtiff5-dev libgif-dev libpng-dev \
    libncurses5-dev texinfo libgccjit-10-dev
```

> Once built, I personally remove all but `build-essential libc6-dev libjpeg62-turbo` packages.

**Step 4. Build Emacs**

I keep my Emacs binary in `~/bin` and Emacs build in `~/emacs`. The build configuration reflects these with `prefix` and `bindir` flags.

> If you want to try using `checkinstall` tool to keep track of your build. Check the [docs](https://help.ubuntu.com/community/CheckInstall).

`cd emacs-27.2`

`./autogen.sh`

```bash
./configure --prefix=/home/user/emacs --bindir=/home/user/bin \
    --with-json --with-gif --with-jpeg --with-png \
    --with-tiff --with-rsvg`
```

> If you'd like you can build Emacs 28 and use it's native compilation feature.
```bash
# For Emacs 28
./configure --prefix=/home/user/emacs --bindir=/home/user/bin \
    --with-native-compilation \
    --with-json --with-gif --with-jpeg --with-png \
    --with-tiff --with-rsvg`
```

`make install`

**Step 5. Clean up**

`make clean`

`make distclean`

#### Uninstalling Emacs

If for some reason you want to uninstall your build, navigate back to the build
source and run:

`make uninstall && rm -rf "~/.emacs.d"`

> If you have deleted the Emacs source code, follow the build steps, 
> and finally run `make uninstall`.

## Installing Doom

**Step 1. Install Doom Dependencies**

`sudo apt-get install ripgrep fd-find`

**Step 2. Install Doom**

`git clone --depth 1 https://github.com/hlissner/doom-emacs ~/.emacs.d`

`cd "~/.emacs.d/bin && doom install"`

_Prompts:_
+ Generate env vars (Y)
+ Install fonts (Y)

**Step 3. Refresh Doom**

If you have a backup of your Doom config, now it's the time to move them to`~/.doom,d/`

Run:

`./doom sync`

### Doom Configuration

There are three configuration files.

`.doom.d/config.el`   - _Custom config, this is your private config._

`.doom.d/init.el`     - _Initializes modules at startup time._

`.doom.d/packages.el` - _Define the packages that you want to install._

You can use `spc f p` to peek into this directory via `projectile`.

### Doom Commands

Doom command line tool lives in `.emacs.d/bin/doom`, and it has some useful commands:

`doom sync`    - _Synchronizes packages and configs._

`doom update`  - _Updates packages._

`doom upgrade` - _Updates Doom itself._

`doom doctor`  - _Helps with diagnosing common issues with your config or environment._

`doom env`     - _Loads your shell env to Doom_

`doom build`   - _Compile packages_

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


#### Search and Destroy

| Search and Destroy                     | Shortcut    | Notes |
|----------------------------------------|-------------|-------|
| Search across project                  | `spc s p`   |       |
| Search another project                 | `spc s S-p` |       |
| Search in directory (recursive)        | `spc s d`   |       |
| Search in another directory(recursive) | `spc s S-d` |       |

After you search, hit `C-c C-e` to activate `wgrep-mode`. Edit the results
and hit `Z Z` to save your changes.


#### Windows

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

#### Buffers

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

| workspaces                | Shortcut          | Notes |
|---------------------------|-------------------|-------|
| Open a new workspace      | `spc tab n`       |       |
| Switch between workspaces | `M + 1` `M + n` |       |
| Save workspace            | `spc tab s`       |       |
| Load workspace            | `spc tab l`       |       |
| Close workspace           | `spc tab c`       |       |

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


### Org-Mode

#### Headlines
| headlines                    | Shortcut            | Notes |
|------------------------------|---------------------|-------|
| Insert an headline           | `*`                 |       |
| Add a headline nested deeper | `**` `***`...       |       |
| Insert headline after        | `C-RET`             |       |
| Move headline up/down        | `M + arrow up/down` |       |
| Promote/Demote headline      | `M + h/j`           |       |


#### Lists
| lists                  | Shortcut            | Notes |
|------------------------|---------------------|-------|
| Ordered list           | `1. 2. 3. ...`      |       |
| Unordered list         | `+`                 |       |
| Insert list item after | `C-RET`             |       |
| Move list item up/down | `M + arrow up/down` |       |

#### Links
| links          | Shortcut  | Notes                          |
|----------------|-----------|--------------------------------|
| Create a link  | `[[]]`    |                                |
| Link selection | `spc m l` | prompt for many types of links |

When you `insert-link` to a selection, you'll get prompted for the type of link you want to
use. Here you can choose to link to a website, another file, another topic, an Emacs command,
or a code snippet that will be evaluated.

#### Content
| content | Shortcut | Notes |
|------------------|----------|-------|
| Inline code      | `==`     |       |
| Code block       | `<s TAB` |       |
| Quotation        | `<q TAB` |       |

#### TODOs
You can suffix your headlines with keywords such as TODO or DONE. It's also possible
to add your custom keywords.

| todos                           | Shortcut                | Notes                       |
|---------------------------------|-------------------------|-----------------------------|
| Add suffix                      | `*** TODO`              |                             |
| View and choose keywords        | `spc m t`               |                             |
| Toggle item complete/incomplete | `RET`                   |                             |
| Increase/Decrease priority      | `Shift + arrow up/down` |                             |
| Search for todo                 | `spc a t`               | Search tags with org-agenda |

Example todo list with progress status:

```org
**** TODO [%]
    - [ ] Brush teeth
    - [ ] Have breakfast
    - [ ] Rock & Roll
```
As you complete the todos with `RET`, the top-level todo will change it's
percentage.

#### Tags
You can add tags to headlines, todo items, and other entries.

| tags           | Shortcut          | Notes                                  |
|----------------|-------------------|----------------------------------------|
| Add tag        | `spc m q`         |                                        |
| Search for tag | `spc a m`         | Search tags with org-agenda            |
| Search for tag | `spc m m s` + `m` | Search and filter with org-sparse-tree |


#### Exporting
**Exporting as Markdown**

In order to export your `.org` file to markdown, `M x` and find `org-md-export-to-markdown`.
You can then fill the export file name prompt and export.

You can also add the following line to your org file and evaluate the command on the fly.
``` org
[[elisp:(org-md-export-to-markdown)]]
```

**Exporting as Github Flavored Markdown**

1. Add `ox-gfm` to your packages.
2. `M x` and look for `org-gfm-export-t- markdown`
You can also add the following line to your org file and evaluate the command on the fly.
``` org
[[elisp:(org-gfm-export-to-markdown)]]
```

**Exporting as HTML**

1. `M x` and look for `org-htmlx-export-to-html`
You can also add the following line to your org file and evaluate the command on the fly.
``` org
[[elisp:(org-html-export-to-html)]]
```

# External Resources

1. [Tecosaur Doom Emacs Config Book](https://tecosaur.github.io/emacs-config/config.html#)
2. [Doom Emacs Cheatsheet](https://gist.github.com/hjertnes/9e14416e8962ff5f03c6b9871945b165)
3. [Zaiste Programming - Emacs Doom Screencast Playlist](https://www.youtube.com/watch?v=rCMh7srOqvw&list=PLhXZp00uXBk4np17N39WvB80zgxlZfVwj)
5. [Seorenn - Emacs Doom Screencast Playlist](https://www.youtube.com/watch?v=zVFqLNps-K0&list=PLPNohcoOBa5FT65hMZL6SkFmbyqFaLe3b)
6. [EmacsCast - Emacs Screencast Playlist](https://www.youtube.com/watch?v=7vC8al1ZZz8&list=PLIrdJT_FTtEZb6Mv_tF9L2AO9XXUNnTyj)
