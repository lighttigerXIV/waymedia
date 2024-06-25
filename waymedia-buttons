#!/usr/bin/env python3

import os
import json
from os.path import expanduser
import subprocess
import re

config_path = f"{expanduser("~")}/.config/waybar"

if os.path.exists(f"{config_path}/config.jsonc"):
    config_path = f"{config_path}/config.jsonc"
else:
    config_path = f"{config_path}/config"

def remove_comments(jsonc_str):
    json_str = re.sub(r'//.*', '', jsonc_str)  # remove single-line comments
    json_str = re.sub(r'/\*.*?\*/', '', json_str, flags=re.DOTALL)  # remove multi-line comments
    return json_str

with open(config_path, "r", encoding="utf-8") as file:
    jsonc_content = file.read()

clean_json_str = remove_comments(jsonc_content)
config_json = json.loads(clean_json_str)


module_configs = config_json.get("custom/waymedia-buttons", {})
play_icon = module_configs.get("play-icon") if "play-icon" in module_configs else "  "
pause_icon = module_configs.get("pause-icon") if "pause-icon" in module_configs else "  "
skip_icon = module_configs.get("skip-icon") if "skip-icon" in module_configs else " 󰒭 "
previous_icon = module_configs.get("previous-icon") if "previous-icon" in module_configs else " 󰒮 "

def get_command_result(command)-> str:
    return subprocess.run(command, shell=True, capture_output=True, text=True).stdout.strip()

metadata = get_command_result("playerctl metadata") 

players = subprocess.run("playerctl --list-all", shell=True, capture_output=True, text=True).stdout.split("\n")

for player in players:
    status = get_command_result(f"playerctl status -p {player}")

    if status != "Stopped" and status != "":
        icon = play_icon if status == "Paused" else pause_icon
        artist = get_command_result("playerctl metadata --format '{{artist}}'")
        title = get_command_result("playerctl metadata --format '{{title}}'")
        
        
        if len(artist) == 0:
            divider = ""


        print(f"{previous_icon} {icon} {skip_icon}", flush=True)
        exit(0)

print("", flush=True)
exit(0)   
