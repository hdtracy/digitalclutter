---
title: Powershell Tidbits
draft: false
tags:
  - powershell
---
# Powershell Tidbits

**Powershell estimation of TOP equivalent on Linux:**
```
Get-Counter '\Process(*)\% Processor Time' | Select-Object -ExpandProperty countersamples| Select-Object -Property instancename, cookedvalue| ? {$_.instanceName -notmatch "^(idle|_total|system)$"} | Sort-Object -Property cookedvalue -Descending| Select-Object -First 25| ft InstanceName,@{L='CPU';E={($_.Cookedvalue/100/$env:NUMBER_OF_PROCESSORS).toString('P')}} -AutoSize
```

---
##### Get MD5 Hash
Go to the folder that contains the file whose MD5 checksum you want to check and verify.  
Command: Type cd followed by the path to the folder.  
Tip: You can drag and drop a folder from Windows Explorer to insert the path.

Type certutil -hashfile <file> MD5.  
<file>: Replace <file> with the filename.  
Tip: You can use the Tab key to have Windows complete the file name.  
Example: Type certutil -hashfile Example.txt MD5 to get the MD5 hash for the file Example.txt


##### Recursive Registry Search 

```
Search-Registry -Hive HKLM -KeyPath 'SOFTWARE' -RegexPattern '.*[Mm]alwar.*' -SearchKeyName -MaximumResults 20 -Recurse -Verbose > results.txt
```

