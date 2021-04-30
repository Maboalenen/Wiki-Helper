Volatility Memory Forensics Framework 
==========

Abstract
--------

>	*Volatility is an open-source memory forensics framework for incident response and malware analysis. *

Source: <a href='https://www.volatilityfoundation.org/26' target='_blank'>Volatility</a> 

Examples/Use Case
----------
**Plugs**

*	[imageinfo](#imageinfo)
*	[kdbgscan](#kdbgscan)
*	[pslist](#pslist)
*	[psscan](#psscan)
*	[pstree](#pstree)
*	[Pstotal](#Pstotal)
*	[malprocfind/psxview](#malprocfind/psxview)   
*	[Processbl](#Processbl) 
*	[Dilllist](#Dilllist) 
*	[Cmdline](#Cmdline)
*	[Getsids](#Getsids) 
*	[Handles](#Handles)
*	[cmdscan/consoles](#cmdscan/consoles)
*	[Netscan](#Netscan)
*	[Chromehistory/iehistory/firefoxhistory](#Chromehistory/iehistory/firefoxhistory)
*	[Malfind](#Malfind)
*	[Ssdt](#ssdt)
*	[Procdump](#procdump)
*	[Memdump](#memdump)
*	[Mimikatz](#Mimikatz) 
*	[FileScan](#FileScan)
*	[Dumpfiles](#Dumpfiles) 
* 	[Modules](#Modules)
*	[Moddump](#Moddump)
*	[Hivelist](#Hivelist)
*	[Hashdump](#Hashdump)
* 	[prefetchpasrser](#prefetchpasrser)
*	[Strings](#Strings)
*	[TimeLiner](#TimeLiner)

### imageinfo
Imageinfo Identify the operating system
```bash
$ vol.py  -f  mem.raw   imageinfo
```
### kdbgscan
Kdbgscan Identify KDBG address 
```bash
$ vol.py -f me.vmem  kdbgscan
```
### pslist
Pslist Print all running processes with th EPROCESS doubly linked list
```bash
$ vol.py -f me.vmem --profile=Win7SP1x86  pslist
```
### psscan
Psscan Scan physical memory for Eprosses but it’s can identify the terminated processes with unlocaked
**Note** : the processes with exit time that is mean the terminated process
```bash
$ vol.py -f me.vmem --profile=Win7SP1x86  psscan
```
### pstree
Pstree print process list as tree collect the perent relationships (using Eprocess linked list)
**Note** Not have the capability to identify terminated or hidden process
```bash
$ vol.py -f me.vmem --profile=Win7SP1x86  pstree
```
### Pstotal
PStotal Comparison between pslist and psscan display the output on graph   
Display the file path
```bash
$ vol.py -f me.vmem --profile=Win7SP0x86 pstotal -c --output=dot --output-file=pstptal.dot
```
### malprocfind/psxview
Malprconfind Automatically identify suspicious system processes
```bash
$ vol.py -f me.vmem --profile=Win7SP0x86 malprocfind          
```
### Processbl
Processbl Baseline analysis (compare processes and loaded DLLs with baseline image)
```bash
$ vol.py -f me.vmem --profile=Win7SP0x86 -B ./baseline-memory/Win7SP1x86-baseline.img processbl -U 2 >>error1.txt
```
### Dilllist
Dilllist Print list loaded dlls for each process ( -p use for the PID for the process)
```bash
$ vol.py -f me.vmem --profile=Win7SP1x86 dlllist -p 4444
```
### Cmdline
Cmdline Display command-line args for each process (Path of process)
```bash
$ vol.py -f me.vmem --profile=Win7SP1x86 cmdline
```
### Getsids
getsids Print ownership SIDs for each process 
```bash
$ vol.py -f me.vmem --profile=Win7SP1x86 getsids -p 4444
```
### Handles
Handles print list opened handles for each process 
**Note** eash process can has hunders or thousands of handles so its better to us the premter with (-p PID ),(-s -t )type Like “File , Port, Muntant “ if you are using -t the option is case.
```bash
$ vol.py -f me.vmem --profile=Win7SP1x86 handles -p 4444
```
### Cmdscan/console
Cmdscan/console Sacn csrss.exe for XP and conhost.exe(win7) for command History and console information.
```bash
$ vol.py -f me.vmem --profile=Win7SP1x86 cmdscan 
```
```bash
$ vol.py -f me.vmem --profile=Winxp consoles
```
### Netscan
Netscan Network artifacts and socket scan working from windows vast and later
 ```bash
$ vol.py -f me.vmem --profile=Win7SP1x86 netscan 
```
### Chromehistory/iehistory/firefoxhistory
"Chromehistory/iehistory/firefoxhistory" recovers fragments of browser history index.dat cache files.
 ```bash
$ vol.py -f me.vmem --profile=Win7SP1x86 iehistory 
```
### Malfind
Malfind to detect the suspicious memory process and dump it to scan with AV or Reverse Engineering Assemble at output.
 ```bash
$ vol.py -f me.vmem  --profile=Win7SP0x86 malfind  |grep -B4 MZ |grep Process
```
### Ssdt
Ssdt System Service Descriptor Table  Kernal (RootKit detection)
**Note** “ntoskrnl.exe or win32k.sys”  this are the two legitimate system file so any process in kirnal using another system fill its seem to be suspicious.
```bash
$ vol.py -f me.vmem --profile=Win7SP0x86 ssdt |egrep -v '(netoskrn|win32k)' 
```
### Procdump
procdump extracting only the Eprocess and and linked list not dump the terminated or unlinked process like psscan
**Note** Parameter -p PID  or -o offset location  or -r Regex  and you can save in directory  --dump-dir=.
```bash
$ Vol.py -f me.vmem --profile=Win7SP0x86  procdump –dump-dir=/output/
$ vol.py -f me.vmem --profile=Win7SP0x86   procdump -p 4444 --dump-dir=test
```  
### Memdump
Memdump To extract all memory resident pages in a process 
**Note** Parameter -p PID  or -r Regex  and you can save in directory  --dump-dir=.
```bash
$ vol.py -f me.vmem --profile=Win7SP0x86  memdump -p 6404 --dump-dir=test
```  
### Mimikatz   
Mimikatz Dump plaintext password from memory (winsows 7 only)
```bash
$ vol.py -f me.vmem --profile=Win7SP0x86  mimikatz
```
### FileScan
FileScan search for file object in memory and Identifies file in memory even if there are no handled (closed file) finds NTFS special files (such as $MFT)that are not present in VAD tree or process handles list.
```bash
$ vol.py -f me.vmem --profile=Win7SP0x86  filescan
```
### Dumpfiles
Dumpfiles  Attempt to Extracting all of the files currently mapped within memory 
**Parameter** -D or –dump-dir=/output/  for save directory -Q physical offset of file_object -r Regular expression 
 -I for case insensitive -n use the orginal file name in output 
**Note** 
to dump specific file you need to use first **filescan** plug to detect the files **offset**
than using **dumpfiles**
```bash
1- $ vol.py -f me.vmem --profile=Win7SP0x86 filescan 
2- $ vol.py -f me.vmem --profile=Win7SP0x86 dumpfiles -n -Q  0x09135278 --dump-dir=. 
$ vol.py -f me.vmem --profile=Win7SP0x86 dumpfiles -n -r spinlock.exe --dump-dir=./    
$ vol.py -f me.vmem --profile=Win7SP0x86 dumpfiles -n -i -r \\.exe –dump-dir=/output
```
### Modules
Modules To view the list of kernel drivers loaded on the system.
```bash
 vol.py -f  vol.py -f me.vmem --profile=Win7SP0x86  modules
 ```
### Moddump 
 Moddump Extract kernel derivers like .sys
 **Note** the premter -b for the Offset you will detect it using modules OR modscan plugs
 ```bash
 $ vol.py -f me.vmem --profile=Win7SP0x86 -b 0xf7c2400 –dump.dir=./output
 ```
### Hivelist
hivelist To locate the virtual addresses of registry hives in memory, and the full paths to the corresponding hive on disk
```bash
$ vol.py -f me.vmem --profile=Win7SP0x86 hivelist
```
### Hashdump
HashDump To extract and decrypt cached domain credentials stored in the registry, (dump the SAM data )
**Note** Note hasdump add the offset for SAM and system and you will be collected with **hivelist ** Plugins 
Virtual (SAM 0xe1035b60 & System 0xe165cb60)
```bash
$ python vol.py -f me.vmem --profile=Win7SP0x86  hashdump  -y 0xe1035b60 -s 0xe165cb60  
```
### Prefetchpasrser
Prefetchpasrser Extract the Prefetch files from memory, even if the Prefetch removed or wipe by attacker,prefetchpasrser , also it will help to reduce the false positives.  
```bash
$ python vol.py -f me.vmem --profile=Win7SP0x86  Prefetchpasrser
```
### Strings
 Strings used to extract English ASCII and Unicode string from data stream
```bash 
1- $ strings -a -td mem.dmp > strings.txt
2- $ strings -a -td -el mem.dmp >> strings.txt
- Translate the string addresses:
3- $ vol.py -f mem.dmp  --profile=Win2008R2SP1x64 strings -s strings.txt > translated.txt
```
### TimeLiner
TimeLiner Collect time information from memory artifacts.
```bash
$ vol.py -f mem.raw –profile=Win7SP1x86 timeliner > timeline.txt
```
