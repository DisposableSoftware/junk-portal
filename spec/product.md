# Product

A starting point for GTK 4 apps on Wayland. Display name **Template App**, binary `tapp`, app ID `io.github.DisposableSoftware.TemplateApp`.

## Requirements

| ID | Requirement | Status |
|----|-------------|--------|
| `PROD-1` | Lightweight and minimal: few dependencies, no libadwaita, fast startup. | done (ongoing constraint) |
| `PROD-2` | Follow a freedesktop/XDG spec wherever one exists for the behaviour (see [integration.md](integration.md)). | done (ongoing constraint) |
| `PROD-3` | Simple toolchain: `cargo` inside a Nix devshell, nothing else. | done |
| `PROD-4` | Easy NixOS integration. | done (see `INT-20`…`INT-24`) |
| `PROD-5` | Every action has a keybinding users can change (see [keybindings.md](keybindings.md)). | done (ongoing constraint) |

## Style guide

The shared look, feel and wording of DisposableSoftware apps is described in the [DisposableSoftware style guide](https://github.com/DisposableSoftware/style-guide). It is a reference, not a requirement: where it and this spec disagree, this spec wins. Look rules that apps adopt from it are `LOOK-n` rows in [appearance.md](appearance.md), each naming the guide page it comes from. The palette is [Catppuccin](https://catppuccin.com), made by the Catppuccin community, and is credited to them wherever it is shown or shipped.

## Non-goals

- No libadwaita. It fights custom theming and transparency.

## Stack constraints

- Rust and gtk4-rs (`gtk4` 0.11 with feature `gnome_49`).
- Use GIO/GLib for anything they provide (XDG dirs, MIME, files, D-Bus) rather than reimplementing it or adding a crate.
- Ask before adding a crate.
- File I/O is async through GIO. The main loop never blocks on I/O.
