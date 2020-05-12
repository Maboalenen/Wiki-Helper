
Kibana Queries and Filters
=========

Abstract
--------
>*is an open-source data visualization and exploration tool used for log and time-series analytics, application monitoring, and operational intelligence use cases*

Source: <a href='https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html#_boolean_queries'  target='_blank'>Kibana</a> 

Where to Acquire
---------
You can install Kibana from the below .

Web site is: <a href='https://www.elastic.co/downloads/kibana' target='_blank'>download Kibana</a>


Search Filters
-------

HTTP redirects
```bash
	http.response.status_code: 302
	type: http AND http.code: 302
```
Strings Queires
```bash
	"test search"
	"Mozilla/5.0"
```
To search for all transactions with the "chunked" encoding:
```bash
	"Transfer-Encoding: chunked"
```
Search specific fields
```bash
	type: http
	status: Error
	method: INSERT
```
Regexp Queries HTTP responses with JSON as the returned value type
```bash
	http.response_headers.content_type: *json
```
To search for slow transactions with a response time greater than or equal to 10ms:
```bash
	event.duration: [10000000 TO *]
```
To search for slow transactions with a response time greater than 10ms:
```bash
	responsetime: {10000000 TO *}
```
Boolean Queries To search for all transactions except MySQL transactions:
```bash
	NOT type: mysql
```
To search for all MySQL INSERT queries with errors:
```bash
	type: mysql AND method: INSERT AND status: Error
```
To search for either INSERT or UPDATE queries with a response time greater than or equal to 30ms:
```bash
	(method: INSERT OR method: UPDATE) AND event.duration >= 30000000
```
Below are some of the common search filters used with Kibana.

This is an example of looking for an logs that contain the string "password":
```bash
password
```
This is an example of looking for logs that contain the name jhenderson stored in a field called user:
```bash
user:jhenderson
```
Note: Sometimes a string needs to be surrounded with double quotes.
```bash
"google.com"
```
This is an example of looking for logs that contain a source port greater than 40000:
```bash
source_port:>40000
```
This is an example of looking for logs that contain a destination IP between 10.0.0.0 and 10.255.255.255:
```bash
destination_ip:[10.0.0.0 TO 10.255.255.255]
```

This is an example of looking for logs that have a field named tls:
```bash
_exists_:tls
```

This is an example of looking for logs that do not have a field named tls:
```bash
-_exists_:tls
```

This is an example of looking for logs that do not have a tag of pci:
```bash
-tags:pci
```
This is an example of looking for logs that are between a specific date:
```bash
@timestamp:[2017-05-01 TO 2017-05-28]
```
Search filters can be combined using (), AND, and OR

This is an example of looking for a network connection sourcing from 192.168.0.1 going to 8.8.8.8:
```bash
source_ip:192.168.0.1 AND destination_ip:8.8.8.8
```

This is an example of looking for a network connection coming from 192.168.0.1 or 192.168.0.2:
```bash
source_ip:192.168.0.1 OR source_ip:192.168.0.2
```

This is an example of looking for a network connection coming from 192.168.0.1 or 192.168.0.2 that is destined for 8.8.8.8:
```bash
(source_ip:192.168.0.1 OR source_ip:192.168.0.2) AND destination_ip:8.8.8.8
```

This is an example of looking for network connections coming from 192.168.0.1 that are not going to 8.8.8.8:
```bash
source_ip:192.168.0.1 AND -destination_ip:8.8.8.8
```
Here is the same example as above that still works:
```bash
source_ip:192.168.0.1 -destination_ip:8.8.8.8
```
This is an example of looking for network connections that are not going to a private IP address:
```bash
-destination_ip:[10.0.0.0 TO 10.255.255.255] -destination_ip:[192.168.0.0 TO 192.168.255.255] -destination_ip:[172.16.0.0 TO 172.16.31.255.255]
```