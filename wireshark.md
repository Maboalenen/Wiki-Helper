
**Wireshark Network Security Monitor** 
========

**Abstract**
-------------

Is a free and open-source traffic Inspection.

Source: <a href='https://www.wireshark.org' target='_blank'>Wireshark</a>

Examples/Use Case
-----------------

**Show only SMTP (port 25) and ICMP traffic**
```bash
 tcp.port eq 25 or icmp
```
**Show only traffic in the LAN No internet **
```bash
 ip.src==192.168.0.0/16 and ip.dst==192.168.0.0/16
```
**Filter on Windows -- Filter out noise, while watching Windows Client**
```bash
 smb || nbns || dcerpc || nbss || dns
```
```bash
 ip.addr == 192.168.1.1
```
**View all http traffic**
```bash
 http
```
**View all flash video stuff**
```bash
 http.request.uri contains "flv" or http.request.uri contains "swf" or http.content_type contains "flash" or http.content_type contains "video"
```
**Show only certain responses**
```bash
 http.response.code == 404
```
**Show only certain http methods**
```bash
 http.request.method == "POST" || http.request.method == "PUT"
```
**Show only certain http methods with response code 200**
```bash
 http.request.method == "POST" and http.request.code == 200
```
**Show only filetypes that begin with "text"**
```bash
http.content_type[0:4] == "text"
```
**Show only javascript**
```bash
http.content_type contains "javascript"
```
**Show all http with content-type="image/(gif|jpeg|png|etc)" §**
```bash
http.content_type[0:5] == "image"
```
**Match HTTP requests where the last characters in the uri are the characters "gl=se":**
```bash
 http.request.uri matches "gl=se$"
``` 
