# pixdecor-mod

A modernized window decorator plugin for the Wayfire compositor.  
It brings pixel-perfect Server-Side Decorations (SSD) that match your system's GTK theme layouts, decoration features, and scale factors, performing all rendering monolithically inside the compositor space using an optimized custom OpenGL shader.

## Acknowledgments

This project is an evolutionary continuation of the original `pixdecor` plugin.

- **Concept and original codebase:** Scott Moreau ([@soreau](https://github.com/soreau))
- **Modernization and GTK theming integration:** [@froloffw7](https://github.com/froloffw7)

## Key Features & Architectural Enhancements

- **Backward compatible:** Existing `pixdecor` configuration option names and the original shaders are preserved.
- **GTK-style decoration shader:** Hardware-accelerated rendering of box shadows, linear gradients, borders, and rounded corners with anti-aliased corner rounding.
- **GTK3 theme loader:** A dedicated GTK theme parser decoupled from the plugin configuration.
- **Reworked rendering pipeline:** Updated title, button, and layout logic with a scale-aware button texture cache supporting fractional display scaling.
- **Unified shade/effect path:** Window shading and overlay effects are handled through a single scene-node hook.
- **Theme configurator:** `gtkdecor_generator` extracts GTK3 theme parameters and generates `pixdecor`-compatible theme data automatically.
- **No external decoration daemon:** All rendering is done server-side directly in the compositor.

## Installation

### Dependencies

Ensure you have `wayfire-dev`, `wlroots`, and standard graphics development headers installed.

### Build

```bash
meson setup build --prefix=/usr
ninja -C build
sudo ninja -C build install
```

Restart Wayfire to reload the plugin environment.

## Usage & Theme Sync

1. Disable any other active window decoration plugins (such as `decoration`, `pixdecor`, etc.) in your `wayfire.ini`.
2. Add `pixdecor-gtk` to the list of plugins in the `[core]` section.
3. Generate theme configuration and assets for your GTK theme:

```bash
./build/configurator/gtkdecor_generator --theme=<theme-name> --dark
```

- `--theme=<theme-name>` — Name of an installed GTK3 theme
- `--dark` — Use the dark color scheme variant

Generated configuration and icons will be stored in:
`~/.config/wayfire/assets/<theme-name>/`

## Screenshots

![Decoration details](https://github.com/user-attachments/assets/...)
*Custom high-contrast test theme with transparency disabled — used to make shadows, borders, and rounded corners clearly visible.*

![Titlebar detail](https://github.com/user-attachments/assets/...)
*Titlebar and button icons on the same test theme, close up at 1:1 scale.*

![Stock Wayfire decor vs pixdecor-mod](https://github.com/user-attachments/assets/...)
*Stock Wayfire `decor` plugin in the foreground, pixdecor-mod with the GTK theme in the background.*

![Ark-Dark SSD/CSD](https://github.com/user-attachments/assets/...)
*Ark-Dark theme, server-side decorations.*

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

Original pixdecor is licensed under the MIT License by Scott Moreau.
