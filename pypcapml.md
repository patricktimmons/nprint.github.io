---
title: pypcapml
has_children: true
# parent: The nPrint Project
nav_order: 4
---

# pypcapml
The ultimate goal of many traffic analysis tasks is to extract information from a set of packets to identify an object, such as an application. `pcapml` creates a standard format for researchers to interface with using standard traffic analysis tools. 

To facilitate faster and simpler traffic analysis pipelines, we've created `pypcapml`, which enables researchers to focus their efforts on new *methods of information extraction* as opposed to dataset interaction, parsing, and metadata attachment. `pypcapml` interacts directly with `pcapml` encoded datasets, exposing an iterator over traffic samples and their associated metadata. `pypcapml` supports returning packets in raw byte sequences, `scapy` packets, or `dpkt` packets.
