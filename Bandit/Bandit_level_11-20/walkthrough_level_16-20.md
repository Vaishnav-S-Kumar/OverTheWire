# Walkthrough for level 16 to 20

method to Access each level: ```ssh banditX@bandit.labs.overthewire.org -p 2220```

X stands for level number

## Level 16

- Credentials will be printed after submitting the password of the current level to the localhost where the port  range from 31000 to 32000. The port would be using SSL/TLS and there is only 1 port which will return the password after submitting the answer
- Use the nmap command to scan all ports and services on the localhost, using the command 
```
nmap -sV -p- localhost

OR 

nmap -A -p- localhost
```
- Identify the port which can used for submitting the password, use the command:
```
openssl s_client -connect localhost:<port>
```

- If the service returns "KEYUPDATE" after entering the password, use the command
```
openssl s_client -connect localhost:<port> -quiet

OR 

openssl s_client -connect localhost:<port> -ign_eof
```
- The SSH key would be printed out, copy the content and paste in file created in your system. Change the permissions of the file, using the command:
```
chmod 700 <file-name>
```

### Explaination
- In nmap,
    - -sV is used for listing the services on the port which are open
    - -p- is used for scanning all the ports 
    - -A is used for aggressive scanning
- In openssl, if the KEYUPDATE comment is returned, -quiet or -ign_eof is used for silencing it and returning the real ouput.
