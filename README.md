<h1 align="center">Template App</h1>

<p align="center">A starting point for GTK 4 apps on Wayland.</p>

> [!WARNING]
> **Certified, artisanal, vibe-coded slop.**
>
> No human has read this code. An AI wrote all of it while a person said "yeah, looks
> good" and pressed Enter a lot.

<!-- template:begin -->
## Using this template

A Rust + GTK 4 + Nix skeleton for building Wayland desktop apps with
[Claude Code](https://claude.com/claude-code), spec first. It is the workflow from
[Junk Drawer](https://github.com/DisposableSoftware/junk-drawer) with the file manager
taken out: a window that says hello, a config file, keybindings, a man page, Nix modules
and the tooling that keeps them honest.

You need Linux and Nix with flakes enabled. Everything else (Rust, GTK 4, sway for the
headless tests) comes from the devshell or `nix-shell` lines in the scripts.

1. Create your repo from this one: **Use this template** on GitHub, or

   ```sh
   gh repo create my-app --public --clone --template DisposableSoftware/gtk-desktop-template
   ```

2. Rename everything:

   ```sh
   scripts/rename.sh "My App" myapp io.github.you.MyApp
   nix develop -c cargo test
   git config core.hooksPath .githooks
   git commit -am "Rename the template to My App"
   ```

   The crate name defaults to the display name in kebab case and the GitHub repo to
   `origin`; pass them as the 4th and 5th arguments to override. The script removes
   itself and this section.
3. Edit `spec/product.md` to say what your app is, then start Claude Code and ask for
   features with `/feature`, fixes with `/bug`, and planned work with `/implement`.

What you get:

- **`spec/`**: every behaviour as a numbered requirement with a status and how it is
  verified. `CLAUDE.md` makes every change go spec first: a `spec:` commit, then code
  with a `Spec: ID` trailer.
- **`/feature`, `/bug` and `/implement`** (`.claude/skills/`): `/feature` drafts the spec
  change and `/bug` reproduces a bug and drafts the spec gap; both ask you to approve
  and implement, or approve the spec only. `/implement` builds the roadmap's approved
  rows in order, one verified commit each.
- **Spec conformance tests** (`src/spec_tests.rs`): the keybinding and config tables in
  the spec are checked against the code, the example config files and the man page.
- **First-run config**: `config.ini` and `keybindings.ini` are created with every default
  commented out, and never overwritten.
- **Headless UI testing** (`scripts/manual/`): `headless.sh` runs a check in a private
  headless sway, D-Bus session and XDG dirs, so it works with the screen locked and never
  touches your desktop. `scales.sh` checks the layout at scales 1, 1.25, 1.5 and 2.
- **Releases**: `release-check.sh` recommends a semver bump from the spec's status
  changes, `release.sh` bumps, tags and drafts notes, the pre-push hook offers to do
  it all when you push main, and `/release` does it from Claude Code.
- **Nix**: package, devshell, `nix flake check` (tests, clippy, rustfmt), overlay, and
  NixOS and home-manager modules.

<!-- template:end -->


## Install

```sh
nix run github:DisposableSoftware/gtk-desktop-template
```

Or as a flake input:

```nix
{
  inputs.template-app.url = "github:DisposableSoftware/gtk-desktop-template";

  # NixOS
  imports = [ inputs.template-app.nixosModules.default ];
  programs.template-app.enable = true;

  # or home-manager, which can also write the settings
  imports = [ inputs.template-app.homeManagerModules.default ];
  programs.template-app = {
    enable = true;
    settings.window.width = 1000;
    keybindings.quit = [ "<Ctrl>q" "<Alt>F4" ];
  };
}
```

## Usage

```sh
tapp            # open a window
tapp --help
man tapp        # every binding and setting
```

Settings live in `~/.config/template-app/config.ini` and keybindings in
`~/.config/template-app/keybindings.ini`. Both are created on first start with every
default commented out; remove the `# ` from a line to change it.

## Development

What the app does is written down in [`spec/`](spec/README.md); see
[`CLAUDE.md`](CLAUDE.md) for how changes are made.

```sh
nix develop                 # cargo, clippy, rustfmt, rust-analyzer, GTK 4
cargo run
cargo clippy --all-targets -- -D warnings
cargo test
nix build                   # ./result/bin/tapp
scripts/manual/headless.sh scripts/manual/smoke.sh
```

## License

MIT, see [LICENSE](LICENSE).

<!-- template:begin -->
## Built with this template

- [cmx](https://github.com/DisposableSoftware/cmx-gtk): a minimal comic reader for `.cbz`
  files, a GTK 4 port of the macOS app.
- [Junk Drawer](https://github.com/DisposableSoftware/junk-drawer): a tiny file manager
  for Hyprland, the app this template was taken from.
- [Downer](https://github.com/DisposableSoftware/downer): a small Markdown viewer for
  Hyprland, in Catppuccin colours.
<!-- template:end -->
