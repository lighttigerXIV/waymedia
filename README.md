<div align="center">
<img src="waymedia.webp">

## Waymedia
</div>

# About
These are two simple modules for waybar. It looks for all active players and when if sees something is playing it will show the proper metadata.
If nothing was found it will hide itself.

# Installation
Clone the repository into a scripts directory in the waybar config directory.

```sh
mkdir -p ~/.config/waybar/scripts/waymedia
git clone https://github.com/lighttigerXIV/waymedia.git ~/.config/waybar/scripts/waymedia
```

# Configuration
## Artist-Title
Add `"custom/waymedia"` to your waybar configuration.

```json
"modules-left": ["custom/waymedia"],
```

### Required configuration
```json
"custom/waymedia": {
    "format": "{icon}{artist}{divider}{title}",
    "exec": "~/.config/waybar/scripts/waymedia/waymedia",
    "interval": 1,
    "limit": 60,
    "on-click": "playerctl play-pause",
    "on-scroll-up": "playerctl next",
    "on-scroll-down": "playerctl previous"
},
```

### Full Configuration
You can customize the play icon, pause icon, the divider and the pattern of how things are displayed.

```json
"custom/waymedia": {
    "format": "{icon}{artist}{divider}{title}",
    "exec": "~/.config/waybar/scripts/waymedia/waymedia",
    "interval": 1,
    "limit": 60,
    "on-click": "playerctl play-pause",
    "on-scroll-up": "playerctl next",
    "on-scroll-down": "playerctl previous",
    "pause-icon": "   ",
    "play-icon": "   ",
    "divider": " - "
},
```

## Buttons
Add `"custom/waymedia-buttons"` to your waybar configuration.

```json
"modules-left": ["custom/waymedia-buttons"],
```

### Required configuration
```json
"custom/waymedia-buttons": {
    "format": "{icon} {artist} - {title}",
    "exec": "~/.config/waybar/scripts/waymedia/waymedia-buttons",
    "interval": 1,
    "on-click": "playerctl play-pause",
    "on-scroll-up": "playerctl next",
    "on-scroll-down": "playerctl previous"
},
```

### Full Configuration
You can customize the buttons too.

```json
"custom/waymedia-buttons": {
    "format": "{icon}{}",
    "exec": "~/.config/waybar/scripts/waymedia/waymedia-buttons",
    "interval": 1,
    "on-click": "playerctl play-pause",
    "on-scroll-up": "playerctl next",
    "on-scroll-down": "playerctl previous",
    "previous-icon": " 󰒮 ",
    "skip-icon": " 󰒭 ",
    "play-icon": "  ",
    "pause-icon": "  "
},
```

# Styling
To style the components use the following selectors
```css
/* For the title/artist */
#custom-waymedia{}

/* For the buttons */
#custom-waymedia-buttons{}
```
