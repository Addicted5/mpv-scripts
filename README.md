# mpv-scripts
A small collection of scripts for the MPV player to make your life a bit better.

## blackout.lua
Couldn't find the "Boss key", but you don't want someone (or simply anyone) to see what you are watching? Just press `b` and whoever is staring at your screen will only wonder why are you watching nothing. And when the intruder is gone just unpause the video (or press `b` again) and enjoy it in privacy.

Notice: it **WILL NOT** minimize MPV window, as it is pretty much impossible to do without writing OS-specific scripts.

Notice: this script relies on setting saturation to the lowest possible value, effectively making video just black. MPV documentation states that this may not work with some VO drivers.

`b` doesn't look too good? Add `KEYBIND script-binding blackout/blackout` to your `input.conf`, `KEYBIND` being any keybind MPV supports.

Another [boss-key script](https://github.com/detuur/mpv-scripts) exists, which actually minimizes the window. Unlike it, blackout doesn't do anything outside of MPV API and makes returning back to video easier (doesn't require switching between windows).

## fuzzydir.lua
Getting bored of moving external audio/subtitles back and forth for MPV to see them? Then surely you are using `sub-file-paths` and `audio-file-paths`. But there is a (big) problem with those wonderful properties: what are you supposed to do when everyone names those directories as they wish? Well, welcome to the horrible mess where you need to add those endless variants (and boy it gets bad when those directories are nested) to those poor properties by your own hands. Doesn't sound too fun or necessary, huh?

So, the solution. This script will read your paths from `mpv.conf`, find those which end with `**` and explode them for good! For example, imagine we have a directory named `subs`, which contains `a` and `b` subdirectories. And those subdirectories contain subtitles which we want to load. Stick `sub-file-paths=subs` to your `mpv.conf` and you won't get anything. But the moment you change it to `sub-file-paths=subs/**` - boom! The script explodes it to `sub-file-paths=subs:subs/a:subs/b` (without messing up your `mpv.conf` and letting MPV handle platform-specific things, of course) and you are good to go. And yes, it works perfectly fine with relative paths. And yes, it is recursive. And yes, it can handle any number of configured paths. And yes, it won't touch non-explodable paths. And yes, you can just use `sub-file-paths=**` and forget all the pain you've had.

Exactly the same thing goes with `audio-file-paths`.

You can control the depth of recursive search in the script by changing `max_search_depth` value, but the default one should be good enough.

## reload.lua
Sometimes you have unstable internet connection, or YouTube server dies, or your computer was sleeping for too long, or whatever. The thing is: you were watching something, you lost the connection, MPV doesn't want to play it further, you don't want to find the video again and then seek it to the moment you were watching. Press `Shift+R` and you're good to go!

`Shift+R` doesn't look too good? Add `KEYBIND script-binding reload/reload` to your `input.conf`, `KEYBIND` being any keybind MPV supports.

Notice: it **WILL NOT** save progress between MPV launches or whatever. It just reopens current video, immediately seeking the moment that was playing before.

## Installation
Copy wanted .lua files to `MPV_CONFIG_PATH/scripts`. Optionally change keybinds and default values inside scripts. You're set to go.
