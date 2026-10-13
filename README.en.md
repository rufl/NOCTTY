# Noctty

[English](README.en.md) · [Português (Brasil)](README.md)

Noctty is the DINX terminal: a Zig-owned UI around a proven terminal-emulation core.

This repository is private and alpha. The initial focus is correct PTY behavior and compatibility with shells, SSH, `vim`, `less`, `tmux` and other TUIs before tabs, transparency or visual effects.

## Goals

- start shells and child processes with correct lifecycle handling;
- resize PTYs, send signals and clean up processes without leaks;
- support VT sequences, Unicode, cursor behavior, colors, alternate screen and scrollback;
- make copy, paste and selection predictable;
- remain compatible with interactive terminal applications;
- integrate with `$TERMINAL`, `.desktop` files, XDG paths and Noctalia;
- remain usable outside the DINX distribution.

## Architecture

```text
Noctty Zig UI
  window · preferences · shortcuts · tabs/panes · theme

Terminal adapter
  input · resize · clipboard · grid · rendering · lifecycle

Proven emulation core
  VT · Unicode · alternate screen · selection · scrollback

System integration
  PTY · shell · processes · signals · environment · working directory
```

The implementation must not reimplement terminal semantics before an existing core has been compared. Initial candidates are libvterm, libtsm and embeddable Ghostty components, subject to public API, build requirements and licensing.

## Noctalia integration

- discovery and launch through `$TERMINAL`;
- shell, working-directory and profile arguments;
- a valid `.desktop` entry;
- theme import through a documented contract;
- optional IPC and plugins, without making Noctalia a startup dependency.

## Initial roadmap

1. PTY, child process and minimal window.
2. Rendering, input, resize, Unicode and scrollback.
3. Shell, TUI, SSH and `tmux` compatibility tests.
4. `$TERMINAL`, `.desktop` and theme integration.
5. Preferences, tabs and panes.

## Documentation

- [Architecture](docs/architecture.md)
- [Compatibility](docs/compatibility.md)

Portuguese (Brazil) versions:

- [Arquitetura](docs/pt-BR/architecture.md)
- [Compatibilidade](docs/pt-BR/compatibility.md)

DINX: [rufl/dinx-alpha](https://github.com/rufl/dinx-alpha)
