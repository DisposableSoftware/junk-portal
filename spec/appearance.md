# Appearance

## Requirements

| ID | Requirement | Status | Verified by |
|----|-------------|--------|-------------|
| `LOOK-1` | Display scale: every size in the spec and in the app's CSS is in logical px, so at scales 1, 1.25, 1.5 and 2 the window has the same layout in logical px, and icons and text are drawn at the display's full resolution, never upscaled. | done | `scripts/manual/scales.sh` (headless at each scale: screenshot; window size in logical px matches `[window]`) |
| `LOOK-2` | One CSS provider at user priority is built at startup from, in order: the flavour's palette file, `@define-color accent`, `@define-color bg` (`base` at the configured opacity), the app's `style.css`, and the user's `style.css` (`LOOK-7`). Rules use palette names, never hex colours. Style guide: palette.md, "How the CSS is assembled". | planned | unit tests on the assembled CSS; manual |
| `LOOK-3` | Four Catppuccin palette files (`latte`, `frappe`, `macchiato`, `mocha`) ship in the app, each unmodified from the style guide's `reference/themes/` with its `/* Catppuccin <flavor> - https://catppuccin.com/palette */` header. Style guide: palette.md, "Flavours". | planned | unit test (every file defines the 26 names and keeps its header) |
| `LOOK-4` | With `flavor = gtk` the palette is derived from the GTK theme once at startup, as the style guide describes, and a fallback provider maps `theme_bg_color`, `theme_fg_color` and `theme_selected_bg_color` to the newer names. Style guide: palette.md, "`flavor = gtk`". | planned | unit tests; manual (screenshot with a GTK theme) |
| `LOOK-5` | Every window, dialogs included, has the CSS class of the binary name, and every rule in the app's CSS starts with `window.<binary>`, so the app never restyles other GTK widgets. Styling is flat: no gradients, shadows or animation, and no libadwaita or header bar. Style guide: principles.md rules 1, 2, 6, 9; components.md, "Conventions". | planned | unit test (every selector in `style.css` is scoped); manual |
| `LOOK-6` | The window background is `@bg`, the flavour's `base` at `[appearance] opacity` (`CONF-7`). Scrolled windows, views and headers are transparent. The UI font is the system font, in `em` sizes. Style guide: principles.md rules 4 and 7. | planned | `scripts/manual/` screenshot at opacity 0.85 and 1.0 |
| `LOOK-7` | `$XDG_CONFIG_HOME/template-app/style.css` is loaded last if it exists, so it can use every palette name and override the app's rules. A missing or unreadable file is not an error. Style guide: palette.md, "How the CSS is assembled". | planned | unit test; manual |
| `LOOK-8` | Selected text keeps a contrast of at least 3:1 against the selection colour for every flavour and accent. Style guide: palette.md, "`flavor = gtk`". | planned | unit test over all flavours and accents |

## Implementation notes

- The [style guide](https://github.com/DisposableSoftware/style-guide) describes the shared look; this file wins on conflict. Catppuccin belongs to the Catppuccin community (https://catppuccin.com).
- Apps made from this template copy the theme module, palette files and `style.css` once they land here. The template's `style.css` stays generic: it styles only the window and its greeting.

- At scale 1, GTK's default font rendering leaves 1px strokes in small text faint. If that matters, set `gtk-font-rendering` to manual with hinted metrics only when every monitor has scale 1 (see Junk Drawer's `theme::set_font_rendering`).
