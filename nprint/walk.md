---
layout: default
title: Usage
has_children: false
parent: nPrint
grand_parent: The nPrint Project
nav_order: 2
---

# Usage

nPrint can be used in a wide variety of ways. A full (and up to date) list of options can be found by running `nprint --help`.

* Collect traffic in real time and print IPv4 / TCP nPrints to stdout

```
nprint -4 -t
```

* Collect traffic in real time and print IPv4 / TCP nPrints to file

```
nprint -4 -t -W test.npt 
```

* Use BPF filters to filter traffic - ICMP nPrints with traffic filtered for only ICMP.

```
nprint -i -W test.npt -f icmp 
```

* Read from a PCAP and nPrint the first 20 payload bytes for each packet to an output file

```
nprint -P test.pcap -W out.npt -p 20 
```

* Take a nPrint file and reverse it into a PCAP

```
nprint -N test.npt -W test.pcap
```

* Include a relative timestamp for each packet, capturing timing information along with selected protocols

```
nprint -R -4 -t 
```
