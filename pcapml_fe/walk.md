---
layout: default
title: Usage
has_children: false
parent: pcapML_FE
grand_parent: The nPrint Project
nav_order: 2
---


# Usage

`pcapml_fe` exposes a simple iterator over a sorted `pcapml` encoded dataset. The iterator can return raw bytes, `scapy` packets or `dpkt` packets. The iterator contains all of the information about a single traffic sample, including the sampleID, the metadata associated with the traffic, the raw packet buffers, and the timestamps associated with each raw packet. 

Below is a full example ([source available here](https://github.com/nprint/pcapml_fe/blob/main/example.py)) of loading and iterating over the `pcapml` encoded DTLS dataset [available for download](https://nprint.github.io/datasets.html)

*Note: The third import provides helpers that can read raw bytes into dpkt or
scapy Ethernet frames (`dpkt_readEther` and `scapy_readEther`, respectively).
The helpers are not strictly necessary to parse pcapML files.*
```python
import argparse
import pcapml_fe
from pcapml_fe_helpers import *

def main():
    '''
    Reads a pcapng file labeled and sorted with pcapml, presenting traffic samples to 
    the user for features to be extracted from. To test the method on a new dataset
    the only needed change is to load in a different dataset
    '''
    parser = argparse.ArgumentParser()
    parser.add_argument('pcapml_dataset')
    args = parser.parse_args()
    
    for traffic_sample in pcapml_fe.sampler(args.pcapml_dataset):
        extract_info(traffic_sample)

def extract_info(traffic_sample):
    '''
    Each sample contains the sampleID, metadata and a list of packets 
    with their associated timestamps
    '''
    print("Sample ID:", traffic_sample.sid)
    print("Sample metadata:", traffic_sample.metadata)
 
    '''
    iterating over the traffic sample (packets and timestamps)
    '''
    for pkt in traffic_sample.packets:
        # Print packet timestamp and raw bytes
        print(pkt.ts, pkt.raw_bytes)

        dpacket = dpkt_readEther(pkt.raw_bytes)
        dpacket.pprint()

        spacket = scapy_readEther(pkt.raw_bytes)
        print(spacket.summary())
        pass

if __name__ == '__main__':
    main()
```
