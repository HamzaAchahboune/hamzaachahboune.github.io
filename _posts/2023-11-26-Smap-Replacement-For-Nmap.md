---
title: "Smap a powerful replacement for Nmap"
date: 2023-11-26 00:00:00 +0000
categories: [Windows]
tags: [Smap]    
author: Hamza Achahboune
layout: post
---

# Smap a powerful replacement for Nmap
# ![img-description](/assets/img/Blog/)
## Introduction


Smap: A Drop-In Replacement For Nmap Powered By Shodan.Io
Smap is a replica of Nmap which uses shodan.io’s free API for port scanning. It takes the same command-line arguments as Nmap and produces the same output which makes it a drop-in replacement for Nmap.

## Features
* Scans 200 hosts per second
* Doesn’t require any account/api key
* Vulnerability detection
* Supports all nmap’s output formats
* Service and version fingerprinting
* Makes no contact to the targets 

## Installation

* You can download a pre-built binary from [here](https://github.com/s0md3v/Smap/releases)
* Smap is also available on AUR as smap-git (builds from source) and smap-bin (pre-built binary).

## Usage
Smap takes the same arguments as Nmap but options other than -p , -h , -o* , -iL are ignored. If you are unfamiliar with Nmap, here’s how to use Smap.

#### Specifying targets
* You can specify targets as follows:
```shell
smap 127.0.0.1 127.0.0.2
```

* You can also use a list of targets, separated by newlines.
```shell
smap -iL targets.txt
```
#### Output
Smap supports 6 output formats which can be used with the -o* as follows. If you want to print the output to the terminal, use hyphen ( -) as filename.

#### Supported formats:

* oX : nmap’s xml format
* oG : nmap’s greppable format
* oN : nmap’s default format
* oA : output in all 3 formats above at once
* oP : IP:PORT pairs separated by newlines
* oS : custom smap format
* oJ : json


#### Specifying ports
Smap scans [1237](https://gist.githubusercontent.com/s0md3v/3e953e8e15afebc1879a2245e74fc90f/raw/1e20288e9bef43b60f7306b6f7e23044dabd9b8c/shodan_ports.txt) ports by default. If you want to display results for certain ports, use the -p option.

```shell
smap -p21-30,80,443 -iL targets.txt
```