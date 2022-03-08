---
layout: default
title: pcapML_FE
has_children: true
# parent: The nPrint Project
nav_order: 4
---

# pcapML_FE
The ultimate goal of many traffic analysis tasks is to extract information from a set of packets to identify an object, such as an application. 
`pcapml` creates a standard format for researchers to interface with using standard traffic analysis tools. To facilitate faster and simpler traffic analysis 
pipelines, we've created pcapML_FE (Feature Explorer), which enables researchers to focus their efforts on new *methods* 
of information extraction* as opposed to dataset interaction, parsing, and metadata attachment. 
`pcapml_fe` interacts directly with `pcapml` encoded datasets, exposing an iterator over traffic samples and their associated metadata. 

