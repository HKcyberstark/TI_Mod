# TI_Mod
Threat Intel with Elastic - Minemeld integration with Elasticsearch

## Threat intelligence feeds

knowledge really is a power. Knowing the methods and tools attackers are most likely to use can help you better prepare your cybersecurity architecture.  Threat intelligence feeds can assist in this process by identifying common indicators of compromise (IOC) and recommending necessary steps to prevent attack or infection.
*Threat intelligence feeds are constantly updating streams of indicators or artifacts derived from a source outside the organization.
*By comparing threat feeds with internal telemetry, you can automate the production of highly valuable operational intelligence.
*Selecting the right feeds isn’t enough. You should be constantly monitoring the ROI of feeds to determine their value to your organization.

## Threat Intelligence Tool

There are various Threat intelligence tools from various security vendors that climb over each other to address the consumer demand for help with the growing number of threats. Architecting an advanced threat intelligence product/tool hugely simplify the process of combining and prioritizing alerts from multiple sources, as well as providing a wide variety of additional benefits.
Opensource feeds are a very good data source in which you can analyse and have the source of feeds that could be of interest to your environment. 

## Prerequisites

*This blog expects to have elastic stack to be readily configured.
*VM/server with minimum 4 GB of RAM

## Tools used

*Mienmeld – Open source Threat feeds developed by paloalto
*Logstash configuration for minelemeld

**Minemeld** is an open-source application that streamlines the aggregation, enforcement and sharing of threat intelligence. 

 *Work flow* 
*collect and aggregate threat intelligence across public, private and commercial intelligence sources
*filter, deduplicate and consolidate metadata across all sources
*Consolidated data is consumed by third party enforcement infrastructure. [Elastic Logstash in our case]

*Logical Flow*

All Threat feeds -- > Input Node --- > Processor Node -- > Logstash output node 

Data sources are feeds called as miner from which IOC are collected . Collected IOC are processed with processor for aggregation and de duplication. Prcocessed IOC are sent to configured output format.

**Input Node**
There are various Source feeds available for IPv4 by default.  Still you can navigate to any of the input node, click new and edit the source of the feed if you wish to collect from any customised feed URL or from your internal environment.

**Processer Node**
IPv4 aggregator processor nodes are available by default. It can be used or the same can be cloned/newly edited with your customised tags and name. 

**Output Node**
We would be using Logstash Output node which will send processed feeds to the Logstash node in a TCP stream with default host to be local host/127.0.0.1 and default port of 5414.
The Logstash output node can be edited as new node to customise the Logstash host and port if needed. 