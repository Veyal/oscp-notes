# Auto Enumeration using AutoRecon

## Goal

Automating initial enumeration so we dont miss anything

## Installation

1. Install all supported packages

```console
sudo apt install seclists curl enum4linux feroxbuster nbtscan nikto nmap onesixtyone oscanner smbclient smbmap smtp-user-enum snmp sslscan sipvicious tnscmd10g whatweb wkhtmltopdf
```

2. Clone repository

```console
git clone https://github.com/Tib3rius/AutoRecon
```

3. Install dependency

```console
pip install -r requirements.txt
```


## How to Use

```console
python3 autorecon.py -ct 4 -cs x.x.x.x
```