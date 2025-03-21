# Basic

## Fonts

- **FiraCode Nerd Font** can be downloaded [here](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.3.0/FiraCode.zip).
- **FiraMono Nerd Font** can be downloaded [here](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.3.0/FiraMono.zip).

You can find more fonts that are optimized for programming or for terminals at [nerdfonts.com](https://www.nerdfonts.com/)

## Code Spell Checker

A basic spell checker that works well with code and documents.

For other languages, corresponding sub-extensions can be installed and activated in `settings.json` as follows:

```json
"cSpell.language": "en,de"
"cSpell.language": "en,de-de"
"cSpell.language": "en,de,de-de"
```

Which country codes are available can be found in the description of the sub-extension.

## Todo Tree

This extension searches the workspace for comment tags such as `TODO` and `FIXME` and displays them in a tree view in the activity bar. The view can be dragged from the activity bar into the Explorer window (or to another location).

### Tags

The following tags are available:

- `INFO` - marks information about a position or an entire section
- `BUG` - marks the location of a bug (there may be a workaround)
- `FIXME` - marks a location that needs to be repaired
- `TODO` - marks a location that has not yet been created or completed
  - `[ ]` - an item in a to-do list that has not yet been completed
  - `[x]` - an item in a to-do list that has already been completed

## Colorful Comments (Refreshed)

This extension helps to highlight comments in the code in color.

The following tags are available:

- `!` red
- `?` cyan
- `^` yellow
- `*` green
- `&` pink
- `~` purple
