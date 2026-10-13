# Noctty compatibility

[English](compatibility.md) · [Português (Brasil)](pt-BR/compatibility.md)

## Desktop contract

- provide a valid `.desktop` entry;
- be discoverable as a terminal through `$TERMINAL`;
- accept a working-directory argument where supported;
- preserve normal desktop opening and keyboard navigation;
- use XDG configuration and cache locations.

## Noctalia contract

Noctalia integration is additive:

1. **Discovery:** Noctalia can find and launch Noctty.
2. **Invocation:** shell, directory and profile arguments behave deterministically.
3. **Theme:** a documented Dinx Theme adapter maps semantic colors and terminal ANSI colors.
4. **Optional IPC:** unavailable or malformed IPC never blocks startup.

Noctty must remain functional when Noctalia is not installed.

## Terminal compatibility matrix

| Area | Acceptance check |
| --- | --- |
| Shell | interactive shell starts and exits cleanly |
| PTY | resize and signal delivery update the child process |
| TUI | `vim`, `less` and `tmux` render and accept input |
| SSH | remote shell and resize work over SSH |
| Unicode | width, combining marks and clipboard text remain correct |
| Scrollback | selection and navigation preserve expected text |
| Alternate screen | applications return to the primary screen without corruption |
| Failure | child-process failure is visible and does not leave a stale session |
