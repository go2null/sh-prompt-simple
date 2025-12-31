<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [sh-prompt-simple](#sh-prompt-simple)
  - [Installation](#installation)
  - [Configuration](#configuration)
    - [SPS_ESCAPE](#sps_escape)
    - [SPS_EXIT_STATUS](#sps_exit_status)
    - [SPS_STATUS](#sps_status)
    - [SPS_WINDOW_TITLE](#sps_window_title)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## sh-prompt-simple

![how the prompt looks in a
window](/screenshots/sh-prompt-simple-demo.png?raw=true)

This is a simple, lightweight, and nice looking prompt that runs quickly
even in very slow shells like MSYS2, Cygwin and WSL.

It shows the short name of the current environment (distribution, OS, etc.,) the
git branch when in a git checkout, the last command exit status (green checkmark
for success and red X mark for non-zero exit) and an optional clean/dirty git
status indicator.

This prompt is compatible with bash, zsh and some other POSIX sh
implementations such as busybox, (d)ash, ksh, etc..

It's based on the [Solarized
Extravagant](https://github.com/magicmonty/bash-git-prompt/blob/master/themes/Solarized_Extravagant.bgptheme)
theme in [bash-git-prompt](https://github.com/magicmonty/bash-git-prompt).

I also made a [PowerShell version of this
prompt](https://gist.github.com/rkitover/61b85690896e29b42897b99c2486477c).

### Installation

```sh
mkdir -p ~/source/repos
cd ~/source/repos
git clone https://github.com/rkitover/sh-prompt-simple
```

Somewhere in your shell startup file, such as `~/.bashrc`, put something like this:

```sh
SPS_STATUS=1
. ~/source/repos/sh-prompt-simple/prompt.sh
```
For `bash`, I also recommend:

```sh
shopt -s checkwinsize
PROMPT_COMMAND='history -a'
```


### Configuration

#### SPS_ESCAPE

The prompt tries to detect bash/busybox/(d)ash/ksh and use zero-width escape
sequences if found. If your shell does not support the `\[ ... \]` zero-width
escape sequences, for example because you didn't turn on the fancy prompt
feature in busybox, you can turn them off by setting:

```sh
SPS_ESCAPE=0
```
, or force them on with:

```sh
SPS_ESCAPE=1
```
If you have a wide enough window, the prompt will work more or less ok without
the escape sequences in shells that don't support them.

#### SPS_EXIT_STATUS

By default, the exit status of the last command will be a green `v` for
success or a red `x` for failure. You can display the actual exit status code
by setting the following:

```sh
SPS_EXIT_STATUS='actual'
```

You can turn it off without re-sourcing any files with:

```sh
unset SPS_EXIT_STATUS
```

#### SPS_STATUS

To show a clean/dirty git status indicator, set this variable:

```sh
SPS_STATUS=1
```
This is disabled by default because it makes the prompt much slower on things
like MSYS2/Cygwin, but it will work fine on Linux. You can also try it on
MSYS2/Cygwin and see if the slowdown is acceptable for you.

You can turn it off without re-sourcing any files, so if it's
particularly slow in a large repository you can just turn it off with:

```sh
unset SPS_STATUS
```

It may be particularly slow when entering a repository, but after that it will
be cached and the prompt will be much faster.

#### SPS_WINDOW_TITLE

By default the window title is set to the domain of the host or the hostname if
on a local network (only two full hostname parts, such as `machine.localnet`.)
To turn this off set:

```sh
SPS_WINDOW_TITLE=0
```
This is a work in progress and I plan to expand this feature to allow for
complex window titles using formats and evaluated variables/commands.
