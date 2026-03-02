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

## Level 17

- The password is in the file password.new and is only the line changed between password.new and password.old
- Since the last level gave the SSH key instead of password, use the command 
```
ssh -i SSH-KEY  <username>@<host> -p <port>
```
- Use ```ls``` to list the contents of the home directory
- Use the ```diff``` command for find the line which was changed
```
diff new_file old_file
```

### Explaination

- ```diff``` is used for comparing to files

## Level 18

- Password is stored in the readme file in the home directory but the terminal cannot be accessed because .bashrc is modified to log out anyone who tries to log in with SSH
- Use the SSH command to execute commands, thus using it to open the contents of the readme file
```
ssh  <username>@ <host> -p <port> <command> <file-name.
```
### Explaination

- SSH allows to execute commands by including it with the SSH command, so using this we can execute commands without entering/ logging into the system

## Level 19

- Password is found in the place where all the passwords of the levels are stored (/etc/bandit_pass), but to access the password of a level, the user should be on that level. For example password of level X can be accessed by the user banditX
- It is told there is a setuid binary, which is a executable file with privileges of the file owner i.e When any user executes this file, the program runs as if it were executed by the owner of the file, not the user who launched it.
- Execute the setuid binary, using the command 
```
./<file-name>
```
- Which shows that if file is executed with a command, it run as if the command is executed by the owner. To see who the owner is, use the command:
```
./<file-name> whoami
```
- After finding the owner name, use the same logic to print the contents of the file containing the password.

## Explaination

- Setuids are executables which runs the execution on behalf of owner, no matter who the user is. Alwasys understand how the setuids are executed and what is its format/methods included in the execution.

