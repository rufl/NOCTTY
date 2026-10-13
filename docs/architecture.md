# Noctty architecture

[English](architecture.md) · [Português (Brasil)](pt-BR/architecture.md)

## Layers

```text
Application UI
  window · preferences · keybindings · tabs/panes · theme

Terminal adapter
  process lifecycle · input · resize · clipboard · terminal grid · rendering data

Terminal-emulation core
  VT parser · screen state · Unicode · alternate screen · selection · scrollback

OS integration
  PTY · child process · signals · environment · working directory
```

The UI owns presentation and user-facing behavior. The adapter owns the boundary that allows the emulation core to be replaced without rewriting the application.

## Adapter contract

The adapter must expose observable behavior for:

- creating and closing a PTY-backed session;
- reading terminal output and sending encoded input;
- resizing rows and columns;
- forwarding signals and reporting process exit;
- reading screen/grid changes for rendering;
- copying and pasting selected text;
- handling an alternate screen without losing the primary screen state.

The contract must not leak a library-specific type into the application layer.

## Core evaluation

Candidates are evaluated with:

- interactive shells and command completion;
- `vim`, `less`, `tmux` and SSH;
- Unicode width, combining marks and input methods;
- alternate-screen transitions;
- selection and large scrollback;
- repeated resize and process exit;
- memory use under long-running sessions.

The selected core is recorded with its version, license, build inputs and compatibility results.

## Application constraints

Noctty must not require elevated privileges. Configuration follows XDG paths. Optional Noctalia integration is loaded defensively and cannot prevent the terminal from starting.
