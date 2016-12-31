---
title: Uber's geo query service
date: 2016-12-30 13:18:52
description: Uber's geo query service (geo divide, index, query system, language)
tags: 
- geo
- Uber
- Go

category: Geo
---
### What
A geofence refers to a human-defined geographic area (or polygon in geometry terms) on the Earth’s surface. 
{% img "/./geofence.png" 200 200 %}

### Language
Node.js vs Go
Why choose Go:
- High-throughput and low-latency requirements
- CPU intensive workload
	Node is optimized for I/O intensive work. Not CPU intensive workload.
- Non-disruptive background loading
	Need to refresh geo data simultaneously, but Node.js is single threaded, background refreshing would affect query performance.
- High developer productivity. Easy to learn for developers.
- Super reliable

### Question
Given a location specified as a lat/lon pair, how do we find which of our many tens of thousands of geofences this location falls into?
Approach 1: scan all polygons with ray casting algorithm -> too slow.
Approach 2: R-tree or S2 -> too complicated
Approach 3 (winner) : two level index: city level geo fence -> inner city geo fence

### System design
To make the system more scalable, Uber choose stateless model where each machine independently has the knowledge of the entire geo space and data.
Deterministic polling schedule periodically polls the latest geo info from global geo fence store. This data is saved in main memory to serve queries and serialized to the local file system for fast bootstrap on service restarts.
{% img "/./go-geofence-service-architecture.png" %}
