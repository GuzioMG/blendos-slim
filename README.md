# my personal blendOS Tracks
These are slightly modified and restructed base BlendOS tracks the way I think is better
## WARNING
These are experimental and might randomly be broken! If such thing occurs, please contact me on discord at `ico278`

* lightweight TTY: `blendos-desktop`
* custom desktop: `blendos-desktop`
* GNOME: `gnome`
* Plasma: `plasma`
* Cinnamon: `cinnamon`
* LXQT: `lxqt`
* MATE: `mate`
* XFCE: `xfce`

## Example GNOME `/system.yaml` (vanilla)

```
repo: 'https://pkg-repo.blendos.co/'

impl: 'https://github.com/ico277/blendos-tracks/raw/main'

track: 'gnome'
```
## Lightweight example (roughly my personal hyprland setup, also untested and just an example)
```
repo: 'https://pkg-repo.blendos.co/'

impl: 'https://github.com/ico277/blendos-tracks/raw/main'

track: 'blendos-desktop'

packages:
    - 'hyprland'
    - 'bemenu'
    - 'waybar'
    - 'playerctl'
    - 'brightnessctl'
    - 'kitty'
    - 'grim'
    - 'slurp'
    - 'wl-clipboard'
    - 'ttf-cascadia-code'
