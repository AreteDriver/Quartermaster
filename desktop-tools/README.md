# EVE Quartermaster - Desktop Tools

Companion utilities for managing EVE Online on desktop platforms.

---

## Linux Multi-Boxing Tools

Lightweight bash scripts for managing multiple EVE client windows on Linux. Tile your clients into a preview grid, switch between them with a rofi menu, and bring any character to fullscreen with a single command.

Perfect for:
- Multi-account players running 3+ clients
- Fleet commanders monitoring multiple characters
- Miners and industrialists managing alt armies
- Anyone tired of Alt+Tab chaos

### Features

- **Window Tiling** - Arrange all EVE clients in a configurable grid
- **Quick Switcher** - Rofi-powered menu to select and focus any character
- **Fullscreen Focus** - Instantly maximize any client to 1920x1080
- **Smart Detection** - Automatically finds EVE windows, ignores the launcher
- **Multi-Monitor Ready** - Configurable offsets for secondary displays
- **Zero Dependencies** - Just wmctrl, xdotool, and rofi

---

## Installation

### Prerequisites

```bash
# Ubuntu/Debian
sudo apt-get install wmctrl xdotool rofi

# Fedora/RHEL
sudo dnf install wmctrl xdotool rofi

# Arch Linux
sudo pacman -S wmctrl xdotool rofi
```

### Setup

```bash
# Navigate to desktop-tools directory
cd desktop-tools/linux

# Make scripts executable
chmod +x *.sh

# Optional: Add to PATH
echo 'export PATH="$PATH:'$(pwd)'"' >> ~/.bashrc
source ~/.bashrc
```

---

## Usage

### Scripts

| Script | Description |
|--------|-------------|
| `eve_tile_all.sh` | Tile all EVE windows in a grid (3 columns default) |
| `eve_switcher.sh` | Interactive rofi/dmenu menu to select and focus a window |
| `eve_focus_main.sh` | Focus a specific window to fullscreen (1920x1080) |

### Tile All Windows

Arrange all running EVE clients in a preview grid:

```bash
./eve_tile_all.sh
```

Before:
```
[EVE Client 1 - Fullscreen]
[EVE Client 2 - Hidden]
[EVE Client 3 - Hidden]
```

After:
```
+--------+--------+--------+
| Alt 1  | Alt 2  | Alt 3  |
+--------+--------+--------+
| Alt 4  | Alt 5  | Alt 6  |
+--------+--------+--------+
```

### Interactive Switcher

Open a menu to select which character to focus:

```bash
./eve_switcher.sh
```

A rofi menu appears listing all EVE windows. Select one and it becomes fullscreen.

### Focus Specific Window

Directly focus a window by its ID:

```bash
# Get window IDs
wmctrl -l | grep "EVE - "

# Focus specific window
./eve_focus_main.sh 0x04800007
```

---

## Configuration

Edit the scripts directly to customize behavior:

### eve_tile_all.sh

```bash
# Grid layout
COLS=3                # Windows per row (3 = 3x3 max grid)
PREVIEW_W=320         # Preview window width (pixels)
PREVIEW_H=180         # Preview window height (pixels)
GAP=10                # Space between windows (pixels)

# Position (for multi-monitor setups)
SCREEN_X=0            # X offset (0 = left edge)
SCREEN_Y=0            # Y offset (0 = top edge)
```

**Example configurations:**

| Setup | COLS | PREVIEW_W | PREVIEW_H |
|-------|------|-----------|-----------|
| 3 clients | 3 | 400 | 225 |
| 6 clients (2 rows) | 3 | 320 | 180 |
| 9 clients (3x3) | 3 | 320 | 180 |
| 4 clients (2x2) | 2 | 480 | 270 |
| Second monitor | 3 | 320 | 180 | + SCREEN_X=1920 |

### eve_focus_main.sh

```bash
# Fullscreen dimensions
MAIN_X=0              # X position (0 = left edge)
MAIN_Y=0              # Y position (0 = top edge)
MAIN_W=1920           # Width (your resolution)
MAIN_H=1080           # Height (your resolution)
```

**Common resolutions:**

| Resolution | MAIN_W | MAIN_H |
|------------|--------|--------|
| 1080p | 1920 | 1080 |
| 1440p | 2560 | 1440 |
| 4K | 3840 | 2160 |
| Ultrawide | 3440 | 1440 |

---

## Keyboard Shortcuts

Bind the scripts to hotkeys for instant access. Example for GNOME:

```bash
# Settings > Keyboard > Custom Shortcuts

# Tile all EVE windows
Name: EVE Tile
Command: /path/to/desktop-tools/linux/eve_tile_all.sh
Shortcut: Super+E

# Open EVE switcher
Name: EVE Switch
Command: /path/to/desktop-tools/linux/eve_switcher.sh
Shortcut: Super+Shift+E
```

For i3/Sway:

```bash
# ~/.config/i3/config
bindsym $mod+e exec ~/path/to/desktop-tools/linux/eve_tile_all.sh
bindsym $mod+Shift+e exec ~/path/to/desktop-tools/linux/eve_switcher.sh
```

---

## Workflow Examples

### Mining Fleet

```
1. Log in all mining characters (Orca + 3 barges)
2. Run: ./eve_tile_all.sh
3. All 4 clients appear in 2x2 preview grid
4. Monitor for gankers across all screens
5. See trouble? Run: ./eve_switcher.sh → Select Orca → Warp fleet
6. Back to previews: ./eve_tile_all.sh
```

### Market Trading

```
1. Log in Jita alt, Amarr alt, Dodixie alt
2. Run: ./eve_tile_all.sh (3x1 row)
3. Watch all three markets simultaneously
4. Price opportunity? ./eve_switcher.sh → focus that alt
5. Execute trade, return to previews
```

---

## Troubleshooting

### "No EVE client windows found"

- Ensure EVE clients are running (not just the launcher)
- Check window titles contain "EVE - " (character name)
- Verify wmctrl sees them: `wmctrl -l | grep EVE`

### Windows not moving

- Ensure wmctrl is installed: `which wmctrl`
- Check you're on X11, not pure Wayland: `echo $XDG_SESSION_TYPE`
- Try running with sudo (for some window managers)

### Rofi menu not appearing

- Install rofi: `sudo apt install rofi`
- Test rofi works: `echo "test" | rofi -dmenu`
- Check no other rofi instance is running

### Wrong resolution

- Edit MAIN_W and MAIN_H in `eve_focus_main.sh`
- Check your resolution: `xrandr | grep '*'`

---

## Platform Notes

- **Platform:** Linux with X11 (Wayland via XWayland may work)
- **Tested on:** Ubuntu 22.04+
- **Requirements:** wmctrl, xdotool, rofi, bash

---

## Integration

These desktop tools complement the EVE Quartermaster mobile app:
- Mobile app for on-the-go character and asset management
- Desktop scripts for active multi-boxing gameplay
- Both share the same EVE Online companion ecosystem
