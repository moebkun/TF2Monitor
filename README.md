# TF2Monitor

An application companion to be run along with you playing Team Fortress 2.

It's purpose is to:

- Collect and present public Steam info about the players you play with. Example info:
  - Steam account creating time
  - Number of TF2 hours
  - Player's public avatar picture
  - Buttons with links to popular sites such as SteamHistory.net and SteamCommunity.com for each player.
- TODO: Keep track of people you know are bots, cheaters, racists and so on.
- TODO: Collect the chat logs from each match you played.
- TODO: Remember/store the demo files for each match.

TODO: The above data will be saved in file(a local [SQLite database](https://www.sqlite.org/) file).

# Screenshot

![Alt text](/screenshots/TF2Monitor.png?raw=true "TF2Monitor")

# What about VAC?

This application does not alter any game file or intervene with the TF2 process and memory in any way. This is completely VAC safe.

All it does is to start TF2 with some flags to tell it to log more info to the `console.log` file, and enable and configure RCON(remote connect) for local applications.

Then the application periodically scans the `console.log` file and sends commands to TF2 over RCON telling it to log info about the players in the server, to votekick cheaters and bots.

Again, this is completely VAC safe.

# Your privacy

Good that you reflected on this! This is after all an application downloaded from the internet, made by someone you probably don't know.

I have no intention nor interest in collecting any of your personal information or any identifiable data.

The source code is available for anyone to inspect.

# How to run and set up

At the moment you need to download the source code and have [The Rust programming language](https://www.rust-lang.org/) installed. After that you go to the folder where this file is located with a command line/terminal prompt and typ `cargo run` and the application will be compiled and started.

First start will complain about a missing `settings.json` file, and a skeleton settings file was created. Open that `settings.json` in a text editor.

## Settings file

The settings file contain information about where to find the TF2 `console.log` file, TF2 RCON settings and your SteamAPI key.

To make it easier, some fields has default values. These you probably don't need to edit.

- RCON ip, port and password. Default values has been filled in.
  - ip: Defaults to `127.0.0.1`, this is your computer
  - port: Defaults to `40434`
  - password: (TODO: Autogenerated and random) is "rconpwd". Change if you want
- Where the TF2 `console.log` file is located. A default value has been filled in, change it if you installed TF2 in a non-standard location outside C:\Program Files.
  - Defaults to `C:\Program Files (x86)\Steam\steamapps\common\Team Fortress 2\tf\console.log`

The SteamAPI key you must do yourself:

- The SteamAPI key.
  - This key is a personal thing and not something I can give you
  - You need to go to https://steamcommunity.com/dev/apikey to create a personal one

## Start TF2 from the app or from Steam?

It's up to you. Some launch options needs to be set in order for the correct logging of data and for the TF2 RCON to be reachable.

In the below launch settings of TF2, if you launch TF2 from Steam or from a command line, the `+rcon_password rconpwd +hostport 40434` needs to match the values from `settings.json`.

# TF2 launch options

If you change rcon-password or port you need to alter the bat file.

`start_tf2.bat`

```
"C:\Program Files (x86)\Steam\steamapps\common\Team Fortress 2\tf_win64.exe" -steam -game tf  -usercon -high +developer 1 +contimes 0 +ip 0.0.0.0 +sv_rcon_whitelist_address 127.0.0.1 +sv_quota_stringcmdspersecond 1000000 +rcon_password rconpwd +hostport 40434 +net_start +con_timestamp 1 -condebug -conclearlog -novid -nojoy -nosteamcontroller -nohltv -particles 1 -console
```

## Explanation

See https://developer.valvesoftware.com/wiki/List_of_Team_Fortress_2_console_commands_and_variables .

These are not found in the above link:

- `-conclearlog` deletes the TF2 log file at startup
-

# Linux support?

I have not tested it but currently the app does not use any platform specifc API.
The UI framework uses glow and there's a note here on libs you might need to install on your Linux machine:
https://crates.io/crates/eframe/0.27.2

# TF2 weapon entities

For future reference.

https://developer.valvesoftware.com/wiki/List_of_Team_Fortress_2_Entities
