---
title: Usage
has_children: false
parent: pcapML_FE
grand_parent: The nPrint Project
nav_order: 2
---


# Usage

`pcapml_fe` exposes a simple iterator over a sorted `pcapml` encoded dataset. The iterator can return raw bytes, `scapy` packets or `dpkt` packets. The iterator contains all of the information about a single traffic sample, including the sampleID, the metadata associated with the traffic, the raw packet buffers, and the timestamps associated with each raw packet. 

Below is a full example of loading and iterating over the `pcapml` encoded DTLS dataset [available for download](https://nprint.github.io/datasets.html)

```
import argparse
import pcapml_fe
from scapy.all import *

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
 
    '''
    iterating over the traffic sample (packets and timestamps)
    Assuming you've imported scapy as 'import scapy.all as scapy'
    you can transform to Scapy packets with 'scapy.Ether(pkt_buf)'
    '''
    print(traffic_sample.sid)
    print(traffic_sample.metadata)

    for pkt in traffic_sample.packets:
        print(pkt.ts, pkt.raw_bytes)
        # pkt = scapy.packet.Packet(pkt.raw_bytes).getlayer(Raw)
        # print(pkt.type)
        # Extract features
```
