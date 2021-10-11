Splunk                                                                                                                                
=====
![image](https://user-images.githubusercontent.com/49055941/133937392-2d5f981a-301a-43f7-a9b0-76141961d314.png)

Abstrict 
-----
> Big data analysis and visualization platform.  
> Splunk is a technology that is used for Captures, indexes, searching, monitoring,   
> visualizing, correlates and analyzing the machine data on a real-time basis. 

What is Splunk query language? 
-------
> SPL is the abbreviation for Search Processing Language 
   designed by Splunk


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

```bash

 
 
 
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
Fast quires to know the data  index and data source 
```bash
| tstats count where index="*" by index source
 ```
 IPlocation
 ```bash
 index="*" | iplocation src_ip | rename Country as Source_Country | iplocation dest_ip | rename Country as Destination_Country | table src_ip Source_Country  dest_ip Destination_Country 
 ```
Microsoft 365 audit logs 
```bash
index="*"  | rex field=AuditData "^(?<F0>[^,]+)," | rex field=AuditData "^(?:[^,]+?,){12}(?<F12>[^,]+?)," | rex field=AuditData "^(?:[^,]+?,){2}(?<F2>[^,]+?)," | rex field=AuditData "^(?:(?:[^,]+)?,){3}(?<F3>[^,]+?)," | rex field=_AuditData "^(?:(?:[^,]+)?,){4}(?<F4>[^,]+?)," | rex field=AuditData "^(?:(?:[^,]+)?,){5}(?<F5>[^,]+?)," | rex field=AuditData "^(?:(?:[^,]+)?,){6}(?<F6>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){7}(?<F7>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){8}(?<F8>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){9}(?<F9>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){10}(?<F10>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){11}(?<F11>[^,]+)?" | stats count by F12 F10
```
Microsoft 365 audit logs IP location (Country)
```bash
index="almirqab" | stats count by AuditData  | rex field=AuditData "^(?<F0>[^,]+)," | rex field=AuditData "^(?:[^,]+?,){12}(?<F12>[^,]+?)," | rex field=AuditData "^(?:[^,]+?,){2}(?<F2>[^,]+?)," | rex field=AuditData "^(?:(?:[^,]+)?,){3}(?<F3>[^,]+?)," | rex field=_AuditData "^(?:(?:[^,]+)?,){4}(?<F4>[^,]+?)," | rex field=AuditData "^(?:(?:[^,]+)?,){5}(?<F5>[^,]+?)," | rex field=AuditData "^(?:(?:[^,]+)?,){6}(?<F6>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){7}(?<F7>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){8}(?<F8>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){9}(?<F9>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){9}(?<F9>[^,]+)?" | rex field=AuditData "^(?:(?:[^,]+)?,){10}(?<F10>[^,]+)?" | rex field=F10 "^(?:(?:[^,]+)?:){1}(?<IP>[^,]+)?" | rex field=IP "\"?(?<IP>[\d\.]+)\"?" | iplocation IP | stats count by  F0 F12 F10 IP Country
```
