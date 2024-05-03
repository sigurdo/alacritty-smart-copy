<p align="center">
    <img width="200" alt="Alacritty Logo" src="https://raw.githubusercontent.com/alacritty/alacritty/master/extra/logo/compat/alacritty-term%2Bscanlines.png">
</p>

<h1 align="center">Alacritty - A fast, cross-platform, OpenGL terminal emulator</h1>

<p align="center">
  <img alt="Alacritty - A fast, cross-platform, OpenGL terminal emulator"
       src="extra/promo/alacritty-readme.png">
</p>

## About this fork

This fork of Alacritty lets you copy and paste with `ctrl+c` and `ctrl+v`, like in most modern Windows and Linux software. If no text is selected, `ctrl+c` sends `SIGINT` like usual. The selection is cleared when you copy with `ctrl+c`. In this way, pressing `ctrl+c` twice will always send minimum one `SIGINT`. Copying without clearing the selection can still be achieved with `ctrl+shift+c`.

Precompiled binaries are available from the [GitHub releases page](https://github.com/sigurdo/alacritty-smart-copy/releases).

On the technical side, a `CopyDynamic` action is added. It copies the selected text and clears the selection. When no text is selected, the keystroke is passed through, thus causing a `SIGINT`.

"Smart copy" was first propsed and rejected already [back in 2018](https://github.com/alacritty/alacritty/issues/1919) for reasons I do not agree with. In 2020, dtheodor provided a [fantastic explanation](https://github.com/alacritty/alacritty/issues/1919#issuecomment-588188924) of why smart copy is such a brilliant solution. A [pull request implementing this feature](https://github.com/alacritty/alacritty/pull/3873) was proposed by ambiso later in 2020, which was also rejected. [Their fork](https://github.com/ambiso/alacritty/tree/master) is sadly outdated now. Therefore, I created this updated fork with the same approach. I plan to keep the fork up to date for as long as I use Alacritty as my daily driver terminal emulator.

The following key bindings are provided by default for Windows, Linux and BSD:

```toml
[[keyboard.bindings]]
key = "V"
mods = "Control"
mode = "~Vi"
action = "Paste"

[[keyboard.bindings]]
key = "C"
mods = "Control"
mode = "~Vi"
action = "CopyDynamic"
```

and in YAML (for Alacritty v0.12 or older),

```yaml
key_bindings:
  - { key: V, mods: Control, mode: ~Vi, action: Paste }
  - { key: C, mods: Control, mode: ~Vi, action: CopyDynamic }
```

## About

Alacritty is a modern terminal emulator that comes with sensible defaults, but
allows for extensive [configuration](#configuration). By integrating with other
applications, rather than reimplementing their functionality, it manages to
provide a flexible set of [features](./docs/features.md) with high performance.
The supported platforms currently consist of BSD, Linux, macOS and Windows.

The software is considered to be at a **beta** level of readiness; there are
a few missing features and bugs to be fixed, but it is already used by many as
a daily driver.

Precompiled binaries are available from the [GitHub releases page](https://github.com/alacritty/alacritty/releases).

Join [`#alacritty`] on libera.chat if you have questions or looking for a quick help.

[`#alacritty`]: https://web.libera.chat/gamja/?channels=#alacritty

## Features

You can find an overview over the features available in Alacritty [here](./docs/features.md).

## Further information

- [Announcing Alacritty, a GPU-Accelerated Terminal Emulator](https://jwilm.io/blog/announcing-alacritty/) January 6, 2017
- [A talk about Alacritty at the Rust Meetup January 2017](https://www.youtube.com/watch?v=qHOdYO3WUTk) January 19, 2017
- [Alacritty Lands Scrollback, Publishes Benchmarks](https://jwilm.io/blog/alacritty-lands-scrollback/) September 17, 2018

## Installation

Alacritty can be installed by using various package managers on Linux, BSD,
macOS and Windows.

Prebuilt binaries for macOS and Windows can also be downloaded from the
[GitHub releases page](https://github.com/alacritty/alacritty/releases).

For everyone else, the detailed instructions to install Alacritty can be found
[here](INSTALL.md).

### Requirements

- At least OpenGL ES 2.0
- [Windows] ConPTY support (Windows 10 version 1809 or higher)

## Configuration

You can find the documentation for Alacritty's configuration in `man 5
alacritty`, or by looking at [the website] if you do not have the manpages
installed.

[the website]: https://alacritty.org/config-alacritty.html

Alacritty doesn't create the config file for you, but it looks for one in the
following locations:

1. `$XDG_CONFIG_HOME/alacritty/alacritty.toml`
2. `$XDG_CONFIG_HOME/alacritty.toml`
3. `$HOME/.config/alacritty/alacritty.toml`
4. `$HOME/.alacritty.toml`

### Windows

On Windows, the config file should be located at:

`%APPDATA%\alacritty\alacritty.toml`

## Contributing

A guideline about contributing to Alacritty can be found in the
[`CONTRIBUTING.md`](CONTRIBUTING.md) file.

## FAQ

**_Is it really the fastest terminal emulator?_**

Benchmarking terminal emulators is complicated. Alacritty uses
[vtebench](https://github.com/alacritty/vtebench) to quantify terminal emulator
throughput and manages to consistently score better than the competition using
it. If you have found an example where this is not the case, please report a
bug.

Other aspects like latency or framerate and frame consistency are more difficult
to quantify. Some terminal emulators also intentionally slow down to save
resources, which might be preferred by some users.

If you have doubts about Alacritty's performance or usability, the best way to
quantify terminal emulators is always to test them with **your** specific
usecases.

**_Why isn't feature X implemented?_**

Alacritty has many great features, but not every feature from every other
terminal. This could be for a number of reasons, but sometimes it's just not a
good fit for Alacritty. This means you won't find things like tabs or splits
(which are best left to a window manager or [terminal multiplexer][tmux]) nor
niceties like a GUI config editor.

[tmux]: https://github.com/tmux/tmux

## License

Alacritty is released under the [Apache License, Version 2.0].

[Apache License, Version 2.0]: https://github.com/alacritty/alacritty/blob/master/LICENSE-APACHE
