# Spawn TTY

## Goal

spawn interactive shell using TTY so we can press 'tab' to use autocomplete

## Linux Server

1. spawn bash on server
```console
python -c "__import__('pty').spawn('/bin/bash')" 
python3 -c "__import__('pty').spawn('/bin/bash')"
```
2. pause current terminal by pressing `Ctrl+Z`
3. back to reverse shell using **stty**
```console
stty raw -echo;fg
```
4. press enter 2x

## Windows Server

Setup nc listener by using rlwrap
```
rlwrap -r nc -lvnp *port*
```