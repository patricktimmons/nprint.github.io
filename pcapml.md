---
layout: default
title: pcapml
nav_order: 3
# parent: The nPrint Project
has_children: true
---

# pcapml

pcapML is a system for improving the reproducability of traffic analysis tasks. pcapML leverages the `pcapng` file format to encode metadata *directly* into raw traffic captures, removing any ambiguity about which packets belong to any given traffic flow, application, attack, or any other item. On the dataset release side, pcapML provides an easy way to encode metadata into raw traffic captures. On the analysis side, pcapML provides a standard dataset format for users to interact with across different datasets.

![pcapML](pcapML.png)
