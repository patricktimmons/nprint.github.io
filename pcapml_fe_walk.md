---
title: Usage
has_children: false
parent: pcapML_FE
grand_parent: The nPrint Project
nav_order: 2
---


# Usage

`pypcapml` exposes a simple iterator over a sorted `pcapml` encoded dataset. The iterator can return raw bytes, `scapy` packets or `dpkt` packets. The iterator contains all of the information about a single traffic sample, including the sampleID, the metadata associated with the traffic, the raw packet buffers, and the timestamps associated with each raw packet. 

Below is a full example of loading and iterating over the `pcapml` encoded DTLS dataset.

```
import sys
import pcapML

def extract_info(sample):
    # Each sample contains the sampleID, metadata,
    # and a list of raw packet buffers with their associated timestamps
    sid = ml_sample[0][1]
    metadata = ml_sample[0][2]

    print(sid, len(sample), label)
    # iterating over the sample
    for index, sid, metadata, pkt_timestamp, pkt_buf in sample:
        pass

for traffic_sample in pcapML.raw_sampler(sys.argv[1]):
    extract_info(traffic_sample)
```
