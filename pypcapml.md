---
title: pypcapml
has_children: true
# parent: The nPrint Project
nav_order: 4
---

# pypcapml
The ultimate goal of many traffic analysis tasks is to extract information from a set of packets to identify an object, such as an application. `pcapml` creates a standard format for researchers to interface with using standard traffic analysis tools. To facilitate faster and simpler traffic analysis pipelines, we've created `pypcapml`, which enables researchers to focus their efforts on new *methods of information extraction* as opposed to dataset interaction, parsing, and metadata attachment. `pypcapml` interacts directly with `pcapml` encoded datasets, exposing an iterator over traffic samples and their associated metadata. `pypcapml` supports returning packets in raw byte sequences, `scapy` packets, or `dpkt` packets.


<!-- For On the analysis side, `pypcapml` leverages the standardized format, exposing a python interface that reads metadata-encoded pcapml output, enabling the user to focus on extracting interesting information from traffic sequences. By building upon a common foundation, ML researchers working on network traffic analyses can spend time and energy on making strides in advancing the state-of-the-art as a community, rather than creating one-off solutions that do not generalize. -->