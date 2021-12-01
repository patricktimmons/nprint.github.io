---
title: Example Walkthrough
has_children: false
parent: nPrint
grand_parent: The nPrint Project
nav_order: 2
---

# Walkthrough

## Usage

nPrint can be used in a wide variety of ways. Examples:

* Collect traffic in real time and print IPv4 / TCP nPrints to stdout

```
nprint -4 -t
```

* Collect traffic in real time and print IPv4 / TCP nPrints to file

```
nprint -4 -t -W test.npt 
```

* Use BPF filters to filter traffic before nPrint: ICMP nPrints with incoming traffic filtered for ICMP only.

```
nprint -i -W test.npt -f icmp 
```

* Read from a PCAP and create a nPrint of the first 20 payload bytes for each packet to stdout:

```
nprint -P test.pcap -p 20 
```

* Take nPrint file and reverse it into a PCAP

```
nprint -N test.npt -W test.pcap
```

* Include a relative timestamp for each packet, capturing timeseries information:

```
nprint -R -4 -t 
```

* Read output from a csv file in hex-encoded format:

```
nprint -C zmap_scan.csv -4 -t -u -i -p 50 -W zmap_scan.npt
```

The full list of options can be found by running: `nprint --help`