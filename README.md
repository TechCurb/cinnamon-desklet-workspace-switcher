# Workspace Grid Desklet

A Cinnamon desklet that displays a clickable grid of workspaces with their names, and highlights the active workspace. Clicking a tile switches to that workspace. The grid auto-sizes and can be configured as auto near-square or fixed rows/cols.

- UUID: `workspace-grid-desklet@cinnamon-docs`
- Does not manage workspace count/layout (reflect-only)
- Uses Cinnamon Settings for configurable options

## Features

- Auto near-square grid layout (default) or fixed rows/cols
- Labels show workspace names with an index fallback
- Active workspace highlighted with a border (outlined pseudo-class)
- Optional scroll-to-switch (by row or by column)
- Resizes tiles automatically when the desklet is resized
- Minimal, theme-friendly styling

## Installation (local)

1) Copy folder into your Cinnamon desklets directory:
- `~/.local/share/cinnamon/desklets/workspace-grid-desklet@cinnamon-docs`

2) If developing from this repository (with the docs project as root), you can symlink:
- `ln -s "$(pwd)/desklets/workspace-grid-desklet@cinnamon-docs" ~/.local/share/cinnamon/desklets/`

3) In Cinnamon Settings > Desklets:
- Enable the Workspace Grid desklet.
- Right-click on the desklet > Configure to adjust settings.

No restart is typically required; Cinnamon will reload desklet resources after changes.

## Settings

- Grid layout mode (Auto near-square | Fixed rows x cols)
- Fixed rows and columns (when Fixed mode is selected)
- Labels: Prefix with index (if name is unavailable, index is the fallback anyway)
- Scroll wheel behavior: Off (default), By column, By row
- Tile spacing (px)

## Behavior Notes

- The desklet does not modify the system’s workspace count or layout. It visualizes and switches among the workspaces defined by Cinnamon.
- Workspace names are read from the workspace, when available. If no name exists, a fallback like "Workspace 1" is used.

## Styling

The desklet uses `stylesheet.css` in this directory. Key classes:
- `.workspace-grid-container`
- `.workspace-grid-table`
- `.workspace-button`
- `.workspace-button:outlined` (active workspace)
- `.workspace-label`

You can customize colors, border, and spacing in the CSS. Inline margins are applied per button to honor the "Tile spacing" setting.

## Development Overview

- `desklet.js` initializes settings, builds a St.Table of tiles, binds events for workspace switching and updates on:
  - workspace switch
  - workspace add/remove
  - settings changes
  - desklet allocation/resize
- Click a tile to call `workspace.activate(global.get_current_time())`.
- Active tile gets the `outlined` pseudo-class (styled in CSS).

## References and Inspirations

- Cinnamon Settings API usage inspired by the example desklet:
  - example: commandResult desklet (for DeskletSettings pattern)
- Workspace grid click and highlight logic inspired by the example applet:
  - example: workspace-grid applet (for GridStyle patterns)

## Testing Checklist

- Multiple workspace counts
- Workspace rename (labels update)
- Add/remove workspaces (grid rebuilds)
- Desklet resize (tiles reflow)
- Toggle settings: layout mode, rows/cols, scroll behavior, spacing
- Active highlight follows current workspace

## Known Limitations

- Workspace name change signal support varies by Cinnamon versions. Names refresh on switches and rebuilds.
- The desklet does not enforce or change grid layout at the WM level (by design).

## License

GPL-2.0-or-later (matches Cinnamon xlet conventions).