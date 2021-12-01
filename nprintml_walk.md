---
title: Usage
has_children: false
parent: nPrintml
grand_parent: The nPrint Project
nav_order: 2
---

# Usage

## Label Files

Label files must always conform to the same CSV structure. The optional header of the CSV is `Item,Label` (case-insensitive). An example label file for a list of pcaps is below.

```
Item,Label # Optional header
anomaly_1.pcap,anomaly
benign_2.pcap,benign
benign_2.pcap,benign
anomaly_2.pcap,anomaly
anomaly_3.pcap,anomaly
...
```

## Directory Usage

nPrintML allows users to supply a directory of PCAPs and a label file to create a full traffic analysis pipeline. Each single PCAP is considered a *single sample* for purposes of machine learning. Using the above label file as `labels.csv` and the directory `pcaps/`, we can run nPrintML on the entire directory in a single call. For this example, we include IPv4 and TCP headers in the nPrints.

`nprintml -a pcap --pcap_dir pcaps/ -L labels.csv -4 -t`

 By default, nprintML will automatically pad every sample with blank nPrints to the maximum PCAP size in the list of labeled fies. This can be avoided with the `-c` flag to use only the first `c` packets in each labeled pcap.
 
`nprintml -a pcap --pcap_dir pcaps/ -L labels.csv -4 -t -c 25`

To summarize, the above command will:

1. run `nprint` on every pcap in the directory with the supplied arguments
2. load all nPrints into memory
3. pad samples to the maximum number of packets found in a single nPrint
4. attach a label to each nPrint
5. train and evaluate a model on the nPrints.


## Single PCAP Usage

nPrintML can also create full traffic analysis pipelines from a single PCAP and a list of labels. To do so, we need to understand `nprint` indexes.

### nPrint Indexes

every nPrint is a CSV file with a specific index. This allows us to load nPrints as dataframes and join labels on the index of the nPrint. By default, the index of each nPrint file is the source IP of each packet in the file. Other options include source ports, destination ports, and traffic flows (5-tuples). The full list of index options is below.

```
0: source IP (default)
1: destination IP
2: source port
3: destination port
4: flow (5-tuple)
```

### Single PCAP labels

When using nprintML in single-pcap mode, we need to supply a label file that maps the index of each nPrint to a label. For example, if we are using the default source IP index, the label file could look like the one below.

```
Item,Label # Optional header
1.2.3.4,device_type1
2.3.4.5,device_type1
4.5.6.7,device_type2
5.6.7.8,device_type3
...
```

### Single PCAP options

By default, nPrintML will perform per-packet machine learning, meaning **every packet is a single sample**. An example of this is below.

`nPrintml -a index -L labels.txt -P traffic.pcap -4 -t`

In many cases, we may want to train models on *sequences* of packets. This is possible using the `--sample_size` argument of nprintML. This will aggregate packets of the same item in `sample_size` groups (in timeseries order).

`nPrintml -a index -L labels.txt -P traffic.pcap -4 -t --sample_size 10`


