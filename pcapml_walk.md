---
layout: default
title: Usage
has_children: false
parent: pcapML
grand_parent: The nPrint Project
nav_order: 2
---

# Walkthrough

## Overview

`pcpaml` standardizes network traffic analysis tasks at the _dataset level_. Rather than focus on a standardized methodology, feature set, or library for combining traffic traces and metadata (such as labels for machine learning tasks), `pcapml` provides a system for directly coupling raw traffic traces and metadata by using the Next Generation PCAP (`pcpang`) format. `pcapng` files can still be read by libraries such as `libpcap`, and inspected using tools such as `tcpdump` or `tshark`. Whereas a `pcap` represents a linked-list of packets, a `pcapng` represents a linked list of _blocks_, which we can use to directly couple metadata and raw packets.

### Sample IDs

`pcapml` attaches a **sampleID** to each packet, enabling us to group packets arbitrarily. With arbitrary packet groupings, we can attach metadata to *any* set of packets, such as a traffic flow, device, application, anomaly, or time window. a sampleID is created by hashing the metadata associated with a given packet.

## Usage

### PcapML Directory Mode

`pcapml` can attach a sample ID and metadata to a directory of `pcap`s, one traffic sample per `pcap` file. Let's walk through an example of this usage type using the [snowflake fingerprintability dataset](https://github.com/kyle-macmillan/snowflake_fingerprintability). This dataset contains a set of DTLS handshakes from four applications, Facebook Messenger, Discord, Google Hangouts, and Snowflake. Each handshake was gathered to understand if Snowflake could be uniqeuly identified from the other services. 

#### Directory Metadata Files

When using `pcapml` in directory mode, metadata files are expected to conform to a simple CSV structure. `pcapml` expects no header on the CSV file, but will skip any line beginnning with a `#`. Each line is expected to be in `filepath,metadata` format. An example metadata file for the snowflake fingeprintability dataset is shown below.

```
facebook-handshake-1.pcap,facebook
discord-handshake-1.pcap,discord
discord-handshake-2.pcap,discord
snowflake-handshake-1.pcap,snowflake
...
...
```

#### Directory Usage

We can then attach the metadata for each handshake in the dataset with a unique _sampleID_ and it's corresponding application metadata in a `pcapng` with using `pcapml` in a single command.

`$ pcapml -D dataset/ -L metadata.csv -W snowflake-dataset.pcapng`

This results in a `pcapng` that can be examined with `tcpdump`.

```
$ tcpdump -r snowflake-dataset.pcapng -c 10
reading from file dtls-dataset.pcapng, link-type EN10MB (Ethernet)
12:58:52.562021 IP 74.125.250.71.19305 > 192.168.7.222.55937: UDP, length 161
12:58:52.562788 IP 192.168.7.222.55937 > 74.125.250.71.19305: UDP, length 618
12:58:52.585452 IP 74.125.250.71.19305 > 192.168.7.222.55937: UDP, length 1119
12:58:52.586333 IP 192.168.7.222.55937 > 74.125.250.71.19305: UDP, length 962
13:07:34.459150 IP 74.125.250.26.19305 > 192.168.7.222.54537: UDP, length 161
13:07:34.460771 IP 192.168.7.222.54537 > 74.125.250.26.19305: UDP, length 617
13:07:34.486225 IP 74.125.250.26.19305 > 192.168.7.222.54537: UDP, length 1119
13:07:34.487034 IP 192.168.7.222.54537 > 74.125.250.26.19305: UDP, length 962
17:12:42.435787 IP 74.125.250.71.19305 > 192.168.7.222.54510: UDP, length 161
17:12:42.438214 IP 192.168.7.222.54510 > 74.125.250.71.19305: UDP, length 705
```

Upon further inspection using `tshark`, we see the _sampleID_ and met directly encoded in the output file, where each handshake receives a unique `sampleID`, leaving no ambiguity on how the metadata is attached to the traffic.

```
$ tshark -r snowflake-dataset.pcapng -T fields  -E header=y -e frame.comment -c 10
9003219589747928972,google
9003219589747928972,google
9003219589747928972,google
9003219589747928972,google
18186043603218801379,google
18186043603218801379,google
18186043603218801379,google
18186043603218801379,google
14792257769479651673,google
14792257769479651673,google
```

### PcapML Single Pcap Mode

`pcapml` can attach a sample ID and metadata to traffic in a single `pcap` by leveraging BPF filters, time windows, or any combination of the two. 

#### Single PCAP Metadata Files

When using `pcapml` in single PCAP mode, metadata files are expected to conform to a simple CSV structure. `pcapml` expects no header on the CSV file, but will skip any line beginnning with a `#`. Each line is expected to be in `Metadata,BPF_filter,Timestamp_start,Timestamp_end` format. Any of these fields can be left blank that are not in use. For example, if we wanted to attach a piece of metadata to every packet from a few IP addresses in a given traffic capture, the metadata file may resemble the one below.

```
windows_device,src 1.2.3.4,,
mac_device,src 5.6.7.8,,
linux_device,src 4.3.2.1,,
...
```

If we wanted to only attach metadata to packets from that IP address in a given time frame we could combine any BPF filter with the timestamp options.

```
windows_device,src 1.2.3.4,2345678,2346789
mac_device,src 5.6.7.8,,
linux_device,src 4.3.2.1,,
...
```

Finally, if we wanted to attach metadata to traffic in an arbitrary time window, say an anomaly, we can simply not supply a BPF filter for the metadata to be attached.

```
anomaly,,2345678,2346789
anomaly,,3456789,4567890
benign,,,1234567,1234578
...
```

#### Single PCAP Usage

We can then attach the metadata for each line in our metadata file in a `pcapng` using `pcapml` in a single command.

`$ pcapml -P traffic.pcap -L metadata.csv -W encoded-dataset.pcapng`

#### PcapML Sorting

By default, any `pcapml` encoded file that is encoded using single pcap mode is left in the original order the traffic was capture in. In many cases, it is beneficial to instead group the packets first by the sampleID that they are associated with and _then_ in time order. `pcapml` can sort the packets of any `pcapml` encoded dataset by sampleID -> timestamp in the same command that metadata encoding is performed.

`$ pcapml -P traffic.pcap -L metadata.csv -W encoded-dataset.pcapng -s`

### PcapML Extraction Mode 

`pcapml` can transform any `pcapng` file encoded using `pcapml` into a directory of `pcap` files, one file per sampleID, using a single command.

`$ pcapml -M snowflake-dataset.pcapng -O output_dir/`

The associated output directory is below.
```
12868490791586055289_google.pcap     1567624542436120405_google.pcap       1912376493094597460_facebook.pcap     4676138587463220727_discord.pcap     7254850485921062848_snowflake.pcap  9982255779078537418_facebook.pcap
12869046855586552312_google.pcap      15679484754686191639_snowflake.pcap  1913144610008489287_snowflake.pcap   4681195497095943526_google.pcap      7256930666031261978_facebook.pcap    9985167304055034928_discord.pcap
1286997930834027255_snowflake.pcap   15679812277643271301_facebook.pcap   1916232746973137357_discord.pcap      4681553453692518285_firefox_facebook.pcap   7259083765404759561_google.pcap     9987359559073017848_discord.pcap
12872114975008852282_google.pcap     15680488968942900640_discord.pcap    1923291248933451411_google.pcap      4682231651136175711_firefox_snowflake.pcap  7270091391588454401_facebook.pcap   9987474006825771582_discord.pcap
1287296956060682578_snowflake.pcap   15684992164591678892_discord.pcap     1925192065339906372_discord.pcap      4683353161259521763_chrome_discord.pcap     7275055456267078471_discord.pcap     9988384164514239661_discord.pcap
12873202627492535975_facebook.pcap   15686837623379429946_snowflake.pcap  1926070980564693651_facebook.pcap    4686331860154165481_chrome_google.pcap      7275947196122656266_facebook.pcap   9988671347025180223_google.pcap
metadata.csv
```

Also note that a `metadata.csv` file is generated which maps each individual `pcap` to the metadata associated with the traffic in that file.

`$ head metadata.csv`

```
File,Metadata
14944434813179707824_google.pcap,google
14395580548679227705_google.pcap,google
14489979562741152699_google.pcap,google
870078443570293459_google.pcap,google
6809604472343037417_google.pcap,google
9649013506394351716_google.pcap,google
16984261106149530861_google.pcap,google
12493399449979137519_google.pcap,google
7073271527767585992_google.pcap,google
```


## Analysis

Although `pcapml` output can be read by tools such as `tshark` or `tcpudmp`, we realize that the crux of traffic analysis tasks involves extracting identifying information from traffic samples. As such, we have built and released [pypcapML](https://nprint.github.io/pypcapml.html) to easily and directly interact with `pcapml` encoded datasets.
