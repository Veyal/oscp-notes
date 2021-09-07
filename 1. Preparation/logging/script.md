# Auto logging using "script" command

## Goal

Log all commands on terminal to file, so we can find the output when screenshot is missing

## How to use

1. Add this script to /home/kali/.zshrc if your kali using zsh
2. always type `exit` to save script

```zsh
if [[ -z $SCRIPT ]]; then
vared -p "Enter the Log Script Name: " -c filename
export SCRIPT=/home/kali/log/$(date +%Y%m%d-%H%M%S).$filename.log
script "$SCRIPT"
fi
```

Add this script to /home/kali/.bashrc if your kali using bash **(not tested)**

```bash
if [[ -z $SCRIPT ]]; then
read -p "Enter the Log Script Name: " filename
export SCRIPT=/home/kali/log/$(date +%Y%m%d-%H%M%S).$filename.log
script "$SCRIPT"
fi
```
