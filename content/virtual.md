+++
Description = ""
date = "2015-09-16T15:46:44-07:00"
draft = false
menu = "main"
title = "Virtual Creations"
type = "page"

+++


## Web design
See [Meta](/meta).

## Network graphs
The igraph R package makes it easy to generate network graphs from various sources.

Anytime there is data of the form:

| thing1 | thing2 |
| :----: |:------:|
| foo    | quaks  |
| bar    | foo    |
| baz    | bar    |
| quaks  | foo    |

one can generate a network graph from it.
If the data is anything other then random, (and perhaps even then) it will make interesting pictures.

An example of such a network graph with relatively few points.

![Network graph of the relationships between Fate/Zero characters](/images/fate-zero-characters-relations.png)

## Wireshark

Using Wireshark to show who's talking to whom on the network.
![Network graph of IP packets as captured by Wireshark](/images/wireshark-ethernet-traffic.png)

## Person data

Network graph showing the connections between names based on people who had them.

Full writeup at [/persondata](/persondata)
