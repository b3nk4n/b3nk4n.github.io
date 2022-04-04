---
title: Record Your Terminal With Terminalizer
author:
  name: Benjamin Kan
categories: [Tools]
tags: [terminalizer, terminal, console, recording]
pin: false
---

Did you ever want to demo a terminal program or remotely explain a sequence of commands to a friend or colleague?
If so, then [terminalizer](https://terminalizer.com/) is a tool for you…

![Terminalizer](/assets/img/posts/2022/terminalizer.gif)
_Example recording with terminalizer_

## Installation

While the installation steps described in the [docs](https://terminalizer.com/install) are not very detailed.
When simply followed them, I ended up with errors. It turned out that [Node.js](https://nodejs.org/en/download/) 16 is not
yet supported. Consequently, I needed to switch to an older version to run this successfully.
Consequently, the following sequence of command did the trick.

```console
$ nvm use 14
$ npm install -g terminalizer
```

Next, as a Mac use with oh-my-zsh, I created and edited a `config.yaml`{: .filepath} to run `zsh` instead of the default `bash`
in the recoreded terminal to effectively get the themese applied in the recording.

```console
$ terminalizer init
$ vim ~/.terminalizer/config.yaml
```

Within the config file, set the [command](https://github.com/faressoft/terminalizer#recording) from `null` to `zsh`.

> Because the `ZSH_THEME="agnoster"` that I usually use has a minor rendering glitch. In the example above,
> the more simplistic theme `ZSH_THEME="robbyrussell"` is used instead.
{: .prompt-tip }

## Usage

The commands for basic usage are explained in detailed in its [docs](https://github.com/faressoft/terminalizer#usage).
However, the most common commands are the following:
- `terminalizer record <name>`: Started a recording and saves a `<name>.yaml`{: .filepath} file.
- `terminalizer play <name>`: Play a recording in the terminal.
- `terminalizer render <name>`: Renders a GIF using the given recording.

> In case you ever end up a warning such as `zsh: command not found: terminalizer` after installing and using `terminalizer`
> successfully, then check your Node version with `node -v`. At the time of writing, there seem to be troubles with `v16.13.1`,
> but no issues with `v14.17.0`.
{: .prompt-warning }
