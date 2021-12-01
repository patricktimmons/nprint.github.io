---
layout: default
title: nPrint
nav_order: 1
# parent: The nPrint Project
has_children: true
---

![nPrint](nprint.png)

nPrint is a standard data representation for network traffic meant to be directly usable with machine learning algorithms, replacing feature engineering for a wide array of traffic analysis problems. We highly encourage you to read the [original nPrint paper](https://arxiv.org/abs/2008.02695). This page is meant as a high level overview of the system. For more advanced usage and details see the [wiki](https://github.com/nprint/nprint/wiki). Finally, if you are looking for a completely automated traffic analysis pipeline using nPrint, we have created [nPrintML](https://github.com/nprint/nprintML). 


## Implemented Protocols

nPrint currently can parse and transform the following protocols, but is easily extendable.

* IPv4
* IPv6 (Fixed Header)
* TCP
* UDP
* ICMP
* Payloads 

# nPrint Machine Learning Pipeline

![pipeline](system.png)

# nPrint structure

nPrints are well-formatted CSV files meant to be used seamlessly in machine learning pipelines, replacing more tedious feature engineering. By default, the first column (index) of each line in a .npt file will be the source IP address for the given packet. Other indexes include destination IPs and ports. Example nprint of the command `nprint -u -p 2 -f udp -c 5`:

```
ip,udp_sport_0,udp_sport_1,udp_sport_2,udp_sport_3,udp_sport_4,udp_sport_5,udp_sport_6,udp_sport_7,udp_sport_8,udp_sport_9,udp_sport_10,udp_sport_11,udp_sport_12,udp_sport_13,udp_sport_14,udp_sport_15,udp_dport_0,udp_dport_1,udp_dport_2,udp_dport_3,udp_dport_4,udp_dport_5,udp_dport_6,udp_dport_7,udp_dport_8,udp_dport_9,udp_dport_10,udp_dport_11,udp_dport_12,udp_dport_13,udp_dport_14,udp_dport_15,udp_len_0,udp_len_1,udp_len_2,udp_len_3,udp_len_4,udp_len_5,udp_len_6,udp_len_7,udp_len_8,udp_len_9,udp_len_10,udp_len_11,udp_len_12,udp_len_13,udp_len_14,udp_len_15,udp_cksum_0,udp_cksum_1,udp_cksum_2,udp_cksum_3,udp_cksum_4,udp_cksum_5,udp_cksum_6,udp_cksum_7,udp_cksum_8,udp_cksum_9,udp_cksum_10,udp_cksum_11,udp_cksum_12,udp_cksum_13,udp_cksum_14,udp_cksum_15,payload_0,payload_1,payload_2,payload_3,payload_4,payload_5,payload_6,payload_7,payload_8,payload_9,payload_10,payload_11,payload_12,payload_13,payload_14,payload_15
5.6.7.8,1,1,0,1,0,1,1,0,1,0,0,0,0,0,1,1,1,1,0,1,0,1,1,0,1,0,0,0,0,0,1,1,0,0,0,0,0,0,0,1,0,0,0,0,1,1,1,1,1,0,0,0,1,1,1,0,0,0,0,0,1,0,0,1,0,0,0,0,0,0,0,0,0,1,0,0,0,1,0,0
4.3.2.1,1,1,1,1,1,0,0,0,1,0,1,1,1,1,1,0,1,1,0,1,0,1,1,0,1,0,0,0,0,0,1,1,0,0,0,0,0,0,0,1,0,0,0,0,1,1,1,1,0,0,1,0,1,0,1,1,1,0,1,0,0,0,0,1,0,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0
1.2.3.4,1,1,1,0,0,0,0,1,0,0,0,1,0,1,0,1,1,1,1,0,0,0,0,1,0,0,0,1,0,1,0,1,0,0,0,0,0,0,0,0,0,0,1,1,0,1,0,0,1,0,0,1,1,0,0,1,0,1,0,1,0,1,0,0,0,1,0,1,0,0,1,1,0,1,1,1,0,0,0,0
4.3.2.1,1,1,0,1,0,1,1,0,1,0,0,0,0,0,1,1,1,1,0,1,0,1,1,0,1,0,0,0,0,0,1,1,0,0,0,0,0,0,0,1,0,0,0,0,1,1,1,1,0,0,0,1,0,1,0,0,0,1,1,0,1,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,1,0,0
1.2.3.4,1,1,1,1,1,0,0,0,1,0,1,1,1,1,1,0,1,1,0,1,0,1,1,0,1,0,0,0,0,0,1,1,0,0,0,0,0,0,0,1,0,0,0,0,1,1,1,1,0,1,1,1,0,1,0,1,0,0,1,1,0,1,1,1,0,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0
```

 

# Citing nPrint
```
@article{holland2020nprint,
  title={nPrint: A Standard Data Representation for Network Traffic Analysis},
  author={Holland, Jordan and Schmitt, Paul and Feamster, Nick and Mittal, Prateek},
  journal={arXiv preprint arXiv:2008.02695},
  year={2020}
}
```


