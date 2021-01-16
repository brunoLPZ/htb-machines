### Curling

Machine with ssh and http ports opened. Password can be obtained by inspecting source code of 
website. The username can be guessed by the articles author in the website. After this we can access the administrator panel of Joomla (administrator url can be obtained with a simple enumeration of the web service). Escalate privileges from Joomla panel is really easy, we can modify any of the php files of the used template. We can use the monkey pentesters PHP reverse shell and we will get a reverse shell as www-data. Then we have a compression challenge to get floris password. After that we can SSH as floris. Finally, we can obtain root flag by taking advantage of a cron job that runs as root. The cron job prints curl output to a file and we can tell curl to load any local file. 

#### Tips

* Always check source code (might contain surprises).
* Record all stuff found (like important files, credentials, opened ports, etc).
* For privilege escalation:
	* Look at execution processes (special attention to root ones)
	* Find command is our friend (find SUID files, find files by name, etc)
