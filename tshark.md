TShark
========

Abstract
--------

> *TShark is a network protocol analyzer. It lets you capture packet data from a live network, or read packets from a previously saved capture file, either printing a decoded form of those packets to the standard output or writing the packets to a file. TShark's native capture file format is pcap format, which is also the format used by tcpdump and various other tools.*

> *Without any options set, TShark will work much like tcpdump. It will use the pcap library to capture traffic from the first available network interface and displays a summary line on stdout for each received packet.*

**Source:** tshark man page
```bash
$ man tshark
```

Where to Acquire
---------

Included with Wireshark.

Examples/Use Case
---------

**Note:** Some of the examples below presume files and paths that might not match your particular system and tool installation.

**Warning:** Examples below use the `-R` syntax for doing display filters. Depending upon the version of tshark installed on your system, you might need to replace `-R` with `-Y`

Read a pcap file:
```bash
$ tshark -r /pcaps/zeus-gameover-loader.pcap
```
Read a pcap, don't resolve names (layers 3 or 4):
```bash
$ tshark -nr /pcaps/zeus-gameover-loader.pcap
```
Read a pcap, use the display filter "http.request.method==GET":
```bash
$ tshark -r /pcaps/zeus-gameover-loader.pcap -R "http.request.method==GET"
```
Read a pcap, show TCP SYN packets not sent to port 80, don't resolve names:
```bash
$ tshark -r /pcaps/zeus-gameover-loader.pcap -n -R "not tcp.port==80 and tcp.flags == 0x0002"
```
Print TCP conversations in a pcap:
```bash
$ tshark -n -r file.pcap -q -z conv,tcp
```
Print HTTP User-Agents in a pcap:
```bash
$ tshark -nr file.pcap -R "http.user_agent" -Tfields -e http.user_agent
```
Print X.509 certificates in a pcap:
```bash
$ tshark -r file.pcap -T fields -R "ssl.handshake.certificate" -e x509sat.printableString
```
Print Name server for HTTPS 
```bash
$ tshark -r file.pcap -T fields -Y 'tcp.dstport ==443 && ssl.handshake.type == 1' -e frame.time -e ip.src -e tcp.srcport -e ip.dst -e tcp.dstport -e ssl.handshake.extensions_server_name 
```
print certificates
```bash
$ tshark -r file.pcap -T fields -Y 'tcp.dstport ==443 && ssl.handshake.certificate'  -E header=y -E separator=/t -E occurrence=a -E aggregator=\| -e x509sat.CountryName  -e x509sat.printableString -e x509sat.uTF8String 

Additional Info
--------------
A printable PDF version of this cheatsheet is available here:
[tshark](pdfs/tshark.pdf)

Cheat Sheet Version
--------------
#### **`Version 1.0`** 
