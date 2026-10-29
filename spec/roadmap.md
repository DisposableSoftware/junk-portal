# Roadmap

The order of approved work: `planned` requirements, and `partial` ones with a known bug from `/bug`. Change it here when priorities change. `/implement` works through this file: the verification backlog first, then the requirements in the order listed.

1. `LOOK-3`: the four Catppuccin palette files.
2. `CONF-6`, `CONF-7`: `[appearance]` keys (`flavor`, `accent`, `opacity`).
3. `LOOK-2`, `LOOK-5`, `LOOK-6`: theme module and the generic scoped `style.css`; the window gets its binary-name class.
4. `LOOK-7`: the user's `style.css`.
5. `LOOK-4`: `flavor = gtk`.
6. `LOOK-8`: selection contrast test.
7. `KEY-5`, `WIN-5`: the `?` shortcut overlay.
8. `INT-42`, `INT-43`: symbolic icon, README shape and Catppuccin credit.

These bring the template in line with the [style guide](https://github.com/DisposableSoftware/style-guide). Apps copy the theme module, palette files and `style.css` from the template afterwards, so keep them generic.

## Verification backlog

Built requirements that are not fully verified. Clear these before starting new planned work.

None.
