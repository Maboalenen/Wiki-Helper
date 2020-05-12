Splunk 
=====


Abstrict 
-----
Splunk is splunk is commercial tools with free limitations edition 500MB per day captures, indexes, and correlates real-time data in a searchable repository from which it can generate graphs, reports, alerts, dashboards, and visualizations.

Source: <a href='https://www.splunk.com'  target='_blank'>Splunk</a> 


Search Command examples 
-------

specific field-value of source IP (src) and destination IP (dst). 
```bash
 search src="10.9.165.*" OR dst="10.9.165.8"
```
 Using boolean and comparison operators this example searches for events with code values of either 10, 29, or 43 and any host that is not "localhost", and an xqp value that is greater than 5
```bash
search (code=10 OR code=29 OR code=43) host!="localhost" xqp>5
```
 An alternative is to use the IN operator, because you are specifying multiple field-value pairs on the same field. The revised search is: 
 ```bash
 search code IN(10, 29, 43) host!="localhost" xqp>5
 ```
 HTTP client and server error status. 
 ```bash
 search host=webserver* (status=4* OR status=5*)
 ```
 An alternative is to use the IN operator, because you are specifying two field-value pairs on the same field. The revised search is: 
 ```bash
 search host=webserver* status IN(4*, 5*)
 ```
 Using the NOT or != comparisons
```bash
search NOT fieldA="value2"
 search fieldA!="value2"
```
top IPs by percent 
```bash
| top clientip |fields - percent  | top clientip
```
top 5 ips
```bash
| top limit=5 c_ip |fields - percent
```
top 50 with the frist 1000 raw data 
```bash
| head 10000 | rex "(?i) GET (?P<clientip>.+?)/\\s+" | top 50 clientip | fields - percent
```
**Clear Queries**

```bash
"failed password" "for valid user"
```
```bash
login OR Failur
```
```bash
ser_ip="192.168..1.1"
```
```bash
ser_ip="192.168..1.0/24"
```
```bash
error OR fail* OR pasword OR login OR failure
```
Decode URL
```bash
| rex mode=sed "s/%[890ABCDEDFabcdef][\d\w]/-/g" | eval decode=urldecode(_raw) | table _raw decode
```
Geolocation IPs
```bash
| iplocation c_ip| stats count by c_ip Country City
```
DNSlookup
```bash
|iplocation ips | lookup dnslookup clientip as ips OUTPUT clienthost as Resolved_hostname | stats count by ips  Resolved_hostname Country
```
Quiery specific fields
```bash 
| stats count by field1,field2,field4
```
Qiures for time taken bigger than 1000
```bash
time_taken>1000  |stats count by time_taken
```