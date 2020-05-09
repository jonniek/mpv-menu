# mpv-menu
Simple mpv menu to launch commands from.

This script allows you to make your own list of commands that you would like to have quick access to without
the need to remember the specific keybind.

### Setup

Put the `menu.lua` file to your `mpv/scripts/` directory. To enable the script you need a `menu.json` file in
your `mpv/script-opts/` directory.  

Example of the structure of the json
```json
[
  {
    "label": "Simply quit mpv",
    "command": ["quit"]
  },
  {
    "label": "Set music profile by running two commands",
    "command": [["apply-profile", "music-disable"], ["show-text", "Music!"]],
  },
  {
    "label": "Increase brightness without closing menu",
    "command": ["add", "brightness", "1"],
    "keep_open": true
  }
]
```

To run arbitrary lua code you need to create a custom script that listens to script-messages.

**mpv/scripts/my_custom_command.lua**
```lua
function my_custom_command(some_data, some_flag)
  -- do something cool
end

mp.register_script_message("my_custom_command", my_custom_command)
```

You can then add it to the menu with the following

```json
[
  {
    "title": "My custom command",
    "command": ["script-message", "my_custom_command", "some_data", true]
  }
]
```
