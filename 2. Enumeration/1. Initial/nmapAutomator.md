# Enumeration using nmapAutomator

## Goal

Automating initial enumeration so we dont miss anything

## Installation

```console
git clone https://github.com/21y4d/nmapAutomator.git
```

## Call anywhere

```console
cd nmapAutomator
sudo ln -s $(pwd)/nmapAutomator.sh /usr/local/bin/
```

## How to use

The old version

```console
nmapAutomator.sh *ip* -A
```

The new version

```console
nmapAutomator.sh -H *ip* -A
```
