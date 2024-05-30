<div align="center">
<img src="waymedia.webp">

## Waymedia
</div>

# About
This is a simple module for waybar. It looks for all active players. When the player isn't stopped it will show the proper metadata. If nothing was found it will hide itself.

# Installation
Clone the repository into a scripts directory in the waybar config directory.

```sh
mkdir -p ~/.config/waybar/scripts/
git clone https://github.com/lighttigerXIV/waymedia.git ~/.config/waybar/scripts/
```

# Configuration
Add `"custom/waymedia"` to your waybar configuration.

```json
"modules-left": ["custom/waymedia"],
```

### Required configuration
```json
"custom/waymedia": {
    "format": "{}",
    "exec": "~/.config/waybar/scripts/waymedia/waymedia",
    "interval": 1,
    "on-click": "playerctl play-pause",
    "on-scroll-up": "playerctl next",
    "on-scroll-down": "playerctl previous"
},
```

### Full Configuration
You can customize the play icon, pause icon, the divider and the pattern of how things are displayed.

```json
"custom/waymedia": {
    "format": "{icon}{}",
    "exec": "~/.config/waybar/scripts/waymedia/waymedia",
    "interval": 1,
    "on-click": "playerctl play-pause",
    "on-scroll-up": "playerctl next",
    "on-scroll-down": "playerctl previous",
    "pause-icon": "   ",
    "play-icon": "   ",
    "divider": " - ",
    "pattern": "{icon}{artist}{divider}{title}"
},
```

# Styling
To style the component simply use the following selector
```css
#custom-waymedia{}
```