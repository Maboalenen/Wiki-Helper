
**Microsoft Tools**


Source: <a href='https://docs.microsoft.com/en-us/sysinternals/' target='_blank'>sysinternals</a> 

**Examples of Tools **
-----------------
**Autorunsc.exe** Windows Sysinternals tool is used to identify areas of persistence Including command line and GUI
Source: <a href='https://docs.microsoft.com/en-us/sysinternals/downloads/autoruns' target='_blank'>autoruns</a> 

```bash
C:\> Autoruns.exe -e
```

**sigcheck.exe** Microsoft tools can be used to gather context ,Adds multiple file hashes .publisher,and virus total checks.
Source: <a href='https://docs.microsoft.com/en-us/sysinternals/downloads/sigcheck' target='_blank'>sigcheckeck</a> 
```bash
C:\> sigcheck.exe -a -h -vs -vt evil.exe
```