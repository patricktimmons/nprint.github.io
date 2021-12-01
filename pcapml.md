---
layout: default
title: pcapml
nav_order: 3
# parent: The nPrint Project
has_children: true
---

# pcapml

Typical network traffic analysis ML pipelines involve gathering network traffic, attaching labels, training models, and (ideally!) public release of the curated dataset for use by other researchers. Yet, unlike other subdisciplines such as natural language processing or image recognition, no standard network traffic dataset format exists for researchers to rely upon. With no standard, datasets are released in multiple ways, each with unique issues, which reduces reproducibility and generalizability of emerging techniques. Given this, results from different studies are difficult, if not impossible, to compare and replicate, even when based on identical source data. 

To remedy this, we have created `pcapml`. `pcapml` standardizes network traffic representation, improving reproducibility by directly coupling metadata and raw traffic traces. For dataset curation, `pcapml` enables researchers to directly encode metadata into raw traffic traces that are readable by classic libraries and tools such as `tcpdump` and `tshark`. 





<!-- In this work we examine the effects that the lack of standardization can have on results in traffic analysis and introduce `pcapml`, a tool that enables standardization of network traffic datasets. `pcapml` enables encoding metadata information directly in raw traffic captures that can still be processed by standard tools and libraries such as `wireshark` or `tcpdump`. `pcapml` also provides researchers with a standardized python framework for interacting with encoded datasets, significantly lowering the barrier to entry for testing new traffic analysis *techniques*.  -->

There will be bugs! Please report any you see.

<!-- ## Why is pcapml needed?

Network traffic analysis has largely directed its focus on applying machine learning techniques to new problems: a typical process involves gathering network traffic, attaching labels to that traffic, training models to identify the traffic, followed with a public release of the curated dataset. Yet--unlike subdisciplines such as natural language processing or image recognition, no standard dataset format exists for researchers to interact with. Datasets are released in a myriad of ways, each with unique issues. Releasing raw traffic with associated metadata released in a separate file requires each researcher that uses the dataset to re-attach metadata to the traffic, creating a significant barrier to entry for reproducing results and testing new methods for the task. Worse, we find this process can cause significant differences in the underlying problems themselves, rendering it all-but impossible to directly compare new methods to previous ones. On the other hand, releasing processed data, such as extracted features, leaves no room for new *techniques* for feature extraction to be tested, stymieing innovation in the field. -->





<!-- ## Research
`pcapml` is a product of our research paper. In it, we highlight performance effects driven by a lack of standardization and how `pcapml` fixes such issues. 


### Cite pcapml
```
@article{holland2020nprint,
  title={nPrint: A Standard Data Representation for Network Traffic Analysis},
  author={Holland, Jordan and Schmitt, Paul and Feamster, Nick and Mittal, Prateek},
  journal={arXiv preprint arXiv:2008.02695},
  year={2020}
}
``` -->