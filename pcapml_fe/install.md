---
layout: default
title: Installation
has_children: false
parent: pcapML_FE
grand_parent: The nPrint Project
nav_order: 1
---

# Installation
pcapML_FE can be installed using `pip` or from source.

## Pip
`pip install pcapml-fe`

## Install From Source

### Supported Operating Systems

* Debian Linux
* macOS

### Dependencies

* [libpcap](https://www.tcpdump.org/) - Packet sniffing
* [python3-dev](https://packages.debian.org/stable/python3-dev) - Header files and library for Python
* [argp](https://www.gnu.org/software/libc/manual/html_node/Argp.html) - Argument parsing

#### Install dependencies on Debian:

`sudo apt-get install libpcap-dev python3-dev`

#### Install dependencies on Mac OS

`brew install argp-standalone`

### Installation 

1. clone repository: `git clone [pcapml_fe]`
2. move to pcapML_FE directory: `cd pcapml_fe`
3. update pcapML submodule: `git submodule update --init --recursive`
3. install pcapML_FE module: `python src/setup.py install`
