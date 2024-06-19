# Rust Powered Linux

## Introduction

If you keep your ear to the ground on linux kernel updates then you may have heard about the Rust programming language being introduced into the codebase.

Unlike previous efforts, which fizzled out, this effort is now firmly established as an alternative language in the linux kernel codebase. This makes for the potential future of the linux kernel to be a very rusty one.

## Why Rust?

Rust drives forward a new way of programming. The simplest explanation for what Rust brings to the table as a technology is high performance with safety. Rust achieves this with ahead of time compilation as well as advanced error checking in the linting part of compilation process.

Rust isn't just limited to just CLI programs either it has libraries for doing all sorts of stuff:

- [Web Assembly Applications](<github.com/yewstack/yew>)
- [Games](<github.com/bevyengine/bevy>)
- [GUI Desktop Applications](<github.com/iced-rs/iced>)
- [CLI Interface](<github.com/mikaelmello/inquire>)

As just a few examples.

## Why Rust Powered Linux Userspace?

As previously stated Rust offers high performance with both memory and thread safety. It is the second part that is particular useful for a "Linux Powered Userspace". 

Applications written in performant languages (besides Rust) suffer from memory leaks and other issues that can compromise security. Rust isn't perfect in this department but it is a marked improvement on what has come before.

Thread safety is also an important advantage. Other performant languages (besides Rust) come with inherent risks associated with multi-threading. Whilst multi-threading isn't a silver bullet combined with some of Rust's functional programming tricks it can significantly speed up a given application in a safe manner and simply won't compile if it is not (unlike C/ C++ which will).

I therefore have more trust in a well written open source Rust application over an alternative C/ C++ application and get to keep similarly high performance.

## Guide

This section will take us through rustifying "Linux Userspace".

### Foreword

This is a guide feel free to include or ignore sections as you see fit.

### Applications

- Cargo
  - cargo-update (cargo-install-update)
- Alacritty
  - Zelij
- Nushell
  - starship
  - tealdeer (tl;dr)
  - bat
  - exa
  - dust
  - fd
  - mcfly
  - ytop
  - bandwhich
  - speedtest-rs
- Cosmic Desktop Environment
- LeftWM
- Development
  - bacon
  - gitui

### Cargo

Cargo is rust's package manager it allows new Rust applications to be downloaded and compiled on the system.

There are a few ways to install cargo.

The main way is through rustup.

> https://rustup.rs/

However you package manager may have it avaliable in repositories to install.

> dnf install cargo
>
> apt install cargo

With cargo installed 

### Cargo Package Maintenance

This package is particularly useful. Cargo doesn't have an inbuilt way of updating installed packages. So I recommend the following tool:

> cargo install cargo-update

Then to run updates run

> cargo install-update --all

This will poll down each installed application and check if a newer one exists then runs:

> cargo install package-name

To update the package.

### Helix

Rust powered vim-like text editor.

> dnf install helix
>
> apt install helix

To use helix open a terminal:

> hx file_to_edit.txt

I recommend running through the helix tutor to learn the various commands required to drive this more advanced text editor. If you are used to vim it is very similar

> hx --tutor

Configuration of helix is done in two files

> [RTFM Option](<https://docs.helix-editor.com/themes.html>)

For the core configuration I recommend using the github_dark theme as this will keep theming cohesion.

In the following file locations

For Unix:

> ~/.config/helix/config.toml

For Windows:

> %AppData%\helix\config.toml

Add the following to the configuration:

> theme = "github_dark"
>
> [editor]
>
> line-number = "relative"
>
> mouse = false
>
>[editor.cursor-shape]
>
> insert = "bar"
>
> normal = "block"
>
> select = "underline"
>
> [editor.file-picker]
>
> hidden = false

Helix also supports programming languages.

> [RTFM Option](<https://docs.helix-editor.com/languages.html>)

This configuration is in the following places

For Unix:

> ~/.config/helix/languages.toml

For Windows:

> %AppData%\helix\languages.toml

The following adds support for the Rust programming language from within helix:

> [language-server.rust-analyzer]
>
> command = "rust-analyzer"
>
> [language-server.rust-analyzer.config]
>
> inlayHints.bindingModeHints.enable = false
>
> inlayHints.closingBraceHints.minLines = 10
>
> inlayHints.closureReturnTypeHints.enable = "with_block"
>
> inlayHints.discriminantHints.enable = "fieldless"
>
> inlayHints.lifetimeElisionHints.enable = "skip_trivial"
>
> inlayHints.typeHints.hideClosureInitialization = false
>
>[language-server.rust-analyzer.config.check]
>
> command = "clippy"

### Alacritty

Alacritty is a terminal that provides a minimalist rust powered terminal.

> dnf install alacritty
>
> apt install alacritty

Configuration is done through a configuration file. Use the following path

> ~/.config/alacritty

Then create a file

> alacritty.toml

Inside this file add the contents of a theme

> [Theme Configurations](<https://github.com/alacritty/alacritty-theme>)

I personally use github_dark if you want a recommendation as it lines up nicely with the helix text editor.

Add the following to the config file

> [font]
>
> size = 24
>
> [[keyboard.bindings]]
> 
> action = "ToggleFullscreen"
>
> key = "F11"
>
> [scrolling]
>
> history = 10000
>
> multiplier = 5

Now for the shell. If you want to use Nushell shell, Zellij multiplexier on top of Alacritty add the following to the configuration file:

> [shell]
>
> args = ["options", "--default-shell", "nu"]
>
> program = "zellij"

Follow the nushell part of the guide to make the "nu" command work if you installed it through cargo.

### Zellij

#### Installation

> cargo install zellij

#### Usage

Open alacritty and type the following

> zellij

This will launch the multiplexier

#### Configuration

Alternatively you can configure this to run on launch. For example ~/.config/alacritty/alarcitty.toml

> [shell]
>
> program = "zellij"

### Starship

#### Installation

> cargo install starship

#### Configuration

Initial configuration of starship can be done like so:

> mkdir ~/.cache/starship
>
> starship init nu | save -f ~/.cache/starship/init.nu

### Nushell

#### Introduction

This is a core part of the rustification of userspace. This will replace your shell with a rust powered shell.

Keep the system default shell as a fallback until you are happy with the migration

#### Installation

Installing nushell

> cargo install nushell

In your terminal of choice there will either be a configuration file or launch option.

> nu

Add nu for nushell to the launch options.

#### Configuration

Allowing cargo packages to run from inside nushell is important to our goal

Navigate to

> ~/config/nushell/env.nu
>
> %AppData%\nushell\env.nu

Add the following line at the bottom of the file

> $env.PATH = ($env.PATH | split row (char esep) | prepend '~/.cargo/bin')

This will add the default install location for cargo so packages can be run in the shell

#### Starship Configuration

In the same env.nu file add the following line to use Starship

> use ~/.cache/starship/init.nu

#### Aliases

You may want to consider some aliases to replace common commands with the rust alternatives we are going to use

Add the following to 

> ~/config/nushell/env.nu
>
> %AppData%\nushell\env.nu

Then add aliases to the file like so:

> # Flatpak Applications
>
> alias github = flatpak run io.github.shiftey.Desktop
>
> # Rust Applications
>
> alias cat = bat
>
> alias ls = exa
>
> alias cu = coreutils
>
> alias grep = rg
>
> alias cat = bat
>
> alias find = fd
>
> alias history = mcfly
>
> alias ps = procs
>
> alias top = ytop
>
> alias network = bandwhich
>
> alias tldr = tldr
>
> alias disk = dust

Keep in mind that string aliases are currently not possible as of version 0.95. The following example WON'T WORK:

> ~alias git-sync = "git add --all; git commit; git pull --rebase; git push"~

## Experimental

These suggestions aren't ready for prime time just yet so use at your own risk

### Coreutils

> cargo install coreutils
