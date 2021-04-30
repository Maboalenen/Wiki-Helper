**TCP-Dump Network Security Monitor**
========
**Abstract**
--------

> * Tcpdump is a common packet analyzer that runs under the command line.prints out a description of the contents of packets on a network interface.*

Source: <a href='https://www.tcpdump.org/' target='_blank'>tcpdump</a>


Examples/Use Case
-----------------

**Write to pcap file** 
```bash
$ tcpdump -w /pcaps/file.pcap
```
**count the number of packets in a particular pcap file** 
```bash
$ tcpdump -nn -r  /pcaps/file.pcap | wc -l 
```
```bash
$ tcpdump -nn -r  /pcaps/file.pcap | head
```
** select only the source IP address with port **
```bash
$ tcpdump -nn -r  /pcaps/file.pcap | cut -f 3 -d " " |head
```
**To filter to just TCP/IP traffic and exclude layer 2 traffic, add the Tcpdump filter of**
```bash
$ tcpdump -nn -r  /pcaps/file.pcap 'tcp or udp' | cut -f 3 -d " " | head
```
** step is to use only the IP address and remove the source port **
```bash
$ tcpdump -nn -r  /pcaps/file.pcap 'tcp or udp' | cut -f 3 -d " " | cut -f 1-4 -d "." | head
```
```bash
$ tcpdump -nn -r  /pcaps/file.pcap 'tcp or udp' | cut -f 3 -d " " | cut -f 1-4 -d "." | sort | uniq | head
```
** to see the destination IP addresses **
```bash
$ tcpdump -nn -r  /pcaps/file.pcap 'tcp or udp' | cut -f 5 -d " " | cut -f 1-4 -d "." | sort | uniq | head
```
** top 10 destination IP **
```bash
$ tcpdump -nn -r  /pcaps/file.pcap 'tcp or udp' | cut -f 5 -d " " | cut -f 1-4 -d "." | sort | uniq -c | sort -nr | head
```
** Tcpdump filter of ‘tcp[13]=2’ which selects only packets with the SYN flag set **
```bash
$ tcpdump -nn -r  /pcaps/file.pcap 'tcp[13]=2' | cut -f 5 -d " " | cut -f 5 -d "." |sort |uniq -c |sort -nr |head
```
** Searching in plain text payloads **
```bash
$ tcpdump -Ann -r  /pcaps/file.pcap 'dst port 25 or dst port 514 or port 110 or dst 21 or dst port 53 or dst port 80' | head -15
```
** Grep to exclude some TLDs **
```bash
$ tcpdump -nn -r  /pcaps/file.pcap 'port 53' |grep -Ev '(com|net|org|gov|mil|arpa)'
```
** filter for names only, not IP addresses **
```bash
$ tcpdump -nn -r  /pcaps/file.pcap 'port 53' |grep -Ev '(com|net|org|gov|mil|arpa)' | cut -f 9 -d " " | grep -E '[a-z]'
```
** Examining HTTP Method **
```bash
$ tcpdump -Ann -r  /pcaps/file.pcap 'dst port 80' | head -15
```
** Removing GET and HEAD methods **
```bash
$ tcpdump -Ann -r  /pcaps/file.pcap 'dst port 80' | grep 'HTTP' | grep -Ev '(GET|HEAD)' |head
```
**  Examing the referer field **
```bash
$ tcpdump -Ann -r  /pcaps/file.pcap 'dst port 80' | grep -i 'referer' |head
```
**User-Agent field**
```bash
$ tcpdump -Ann -r  /pcaps/file.pcap 'dst port 80' | grep -Ei 'user-agent' |sort |uniq -c | sort -nr |head -15
```
**for irregular user-agnet**
```bash
$ tcpdump -Ann -r  /pcaps/file.pcap 'dst port 80' | sed -n '/python-request/,$p' | head
```
**Using the “--context=5"**
```bash
$ tcpdump -Ann -r  /pcaps/file.pcap 'dst port 80' | grep -Ei '/python-request/' --context=5 | head 
```













