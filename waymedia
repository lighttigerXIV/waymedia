#!/usr/bin/env python3

import os
import json
from os.path import expanduser
import subprocess
import re

config_path = f"{expanduser('~')}/.config/waybar"

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

module_configs = config_json.get("custom/waymedia", {})
pause_icon = module_configs.get("pause-icon", "   ")
play_icon = module_configs.get("play-icon", "   ")
divider = module_configs.get("divider", " - ")
format = module_configs.get("format", "{icon}{artist}{divider}{title}")
limit = module_configs.get("limit", 60)

def get_command_result(command) -> str:
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

        text = format.replace("{icon}", icon).replace("{title}", title).replace("{divider}", divider).replace("{artist}", artist).strip().replace("&", "&amp;").replace("{}", "")

        if len(text) > limit:
            text = f"{text[:limit - 3]}..."
            
        print(text, flush=True)
        exit(0)

print("", flush=True)
exit(0)

