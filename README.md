# Sway - ansible role for user setup

This role installs and creates config for sway, swayidle, waybar.

A lot of stuff can be changed by using variables. You might want to take a look into the default vars or the templates

# Example changed vars for my stuff

```
---
sway_workspaces:
  - index: "1"
    name: "Side"
    output: "DP-2"
    app_assignment:
      - "org.keepassxc.KeePassXC"
  - index: "2"
    name: "Main"
    output: "DP-1"
  - index: "3"
    name: "Mail"
    output: "DP-1"
    app_assignment:
      - "thunderbird"
  - index: "4"
    name: "Scripting"
    output: "DP-1"
  - index: "5"
    name: "Music"
    output: "DP-2"
  - index: "6"
    name: "Scripting 2"
    output: "DP-2"

sway_outputs:
  - name: "DP-1"
    resolution: "3440x1440"
    position: "1920 0"
    focus: true
  - name: "DP-2"
    resolution: "1920x1080"
    position: "0 0"

sway_inputs:
  - name: "type:keyboard"
    data: |-
      xkb_layout "neolight"
      xkb_variant "de"

sway_floating_windows:
  - app_id: "org.pulseaudio.pavucontrol"
    state: true
  - app_id: "org.gnome.clocks"
  - app_id: "com.nextcloud.desktopclient.nextcloud"

sway_autostart_applets:
  - "nm-applet"

sway_autostart_programs:
  - "firefox"
  - "thunderbird"
  - "tilix"
  - "nextcloud"
  - "/usr/libexec/gsd-xsettings"
  - "keepassxc"

sway_waybars:
  - name: "main"
    display: "DP-1"
    modules_left:
      - "sway/workspaces"
    modules_center:
      - "sway/mode"
    modules_right:
      - "idle_inhibitor"
      - "pulseaudio"
      - "network"
      - "cpu"
      - "memory"
      - "temperature"
      - "custom/weather"
      - "sway/language"
      - "clock"
      - "tray"
    clock_interval: '1'
  - name: "side"
    display: "DP-2"
    height: "30"
    modules_left:
      - "sway/workspaces"
    modules_center:
      - "sway/mode"
    modules_right:
      - "idle_inhibitor"
      - "pulseaudio"
      - "network"
      - "cpu"
      - "memory"
      - "temperature"
      - "sway/language"
      - "clock"
      - "tray"
    clock_interval: '1'

sway_idle_events: |-
  timeout 240 'notify-send -u normal -t 5000 "IDLE NOTIFICATION" "You idled for 4 minutes"' \
  timeout 280 'notify-send -u critical -t 5000 "IDLE NOTIFICATION" "Lock in 20 seconds"' \
  timeout 300 'swaylock'
sway_idle_systemd_enabled: true

sway_mediaplayer_mode_enabled: true
sway_volumemanager_mode_enabled: true

sway_appkeys:
  - keys: "Print"
    command: "grimshot --notify copy area"

sway_lock_images:
  - display: "DP-2"
    location: "/home/dhoessl/.config/swaylock/milkyway1920x1080.jpg"
  - display: "DP-1"
    location: "/home/dhoessl/.config/swaylock/milkyway3440x1440.jpg"
...
