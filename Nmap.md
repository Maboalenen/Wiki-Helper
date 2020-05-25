**Nmap**
===========


Abstract
--------
Nmap is a free and open-source network scanner


Source: <a href='https://nmap.org' target='_blank'>Nmap</a>

Examples 
--------
Scan a single IP
```bash 
$ nmap 192.168.1.1
```
Scan a host
```bash 
$ nmap www.host.com
```
Scan a range of IPs
```bash 
$ nmap 192.168.1.1-20
```
Scan a subnet
```bash 
$ nmap 192.168.1.0/24
```
Scan targets from a text file
```bash 
$ nmap -iL list-of-ips.txt
```
Scan a single Port
```bash 
$ nmap -p 22 192.168.1.1
```
Fast port scan (100 ports) 
```bash 
$ nmap -F 22 192.168.1.1
```
Scan a range of ports
```bash 
$ nmap -p 1-100 192.168.1.1
```
Scan all 65535 ports
```bash 
$ nmap -p- 192.168.1.1
```
Detect OS and Services
```bash 
$ nmap -A 192.168.1.1
```
Standard service detection
```bash 
$ nmap -sV 192.168.1.1
```
More aggressive Service Detection
```bash 
$ nmap -sV --version-intensity 5 192.168.1.1
```
Get help for a script
```bash 
$ nmap --script-help=ssl-heartbleed
```
Scan using default safe scripts
```bash 
$ nmap -sV -sC 192.168.1.1
```
Scan using a specific NSE script
```bash 
$ nmap -sV -p 443 –script=ssl-heartbleed.nse 192.168.1.1
```
Scan using default safe scripts
```bash 
$ nmap -sV -sC 192.168.1.1
```
Scan with a set of scripts
```bash 
$ nmap -sV --script=smb* 192.168.1.1
```
Find Information about IP address
```bash 
$ nmap --script=asn-query,whois,ip-geolocation-maxmind 192.168.1.0/24
```
Save default output to file
```bash 
$ nmap -oN outputfile.txt 192.168.1.1
```
Save in all formats
```bash 
$ nmap -oA outputfile 192.168.1.1
``` 