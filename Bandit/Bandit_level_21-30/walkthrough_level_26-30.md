``# Walkthrough for level 26 to 30

method to Access each level: ```ssh banditX@bandit.labs.overthewire.org -p 2220```

X stands for level number

## Level 26

- Password for the next level is not mentioned in the description but in the previous challenge, it is mentioned the shell of this level is not /bin/bash, but something else. 
- First, find the shell used in this level by again logging into bandit25 and using the command
```
cat /etc/passwd | grep "username"

[username] of the level
``` 
- Find the shell used and what the shell contains, Since the shell used contains execution of a text file using more.
```
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```
- Minimize the terminal/reduce the size of the terminal window so that when you login using ssh, The shell wouldn't exit automatically.
- Use the ```v``` key to switch to vim and use the following command
```
:set shell=/bin/bash
:shell
```
- Use the ```ls``` to list the contents of the home directory and it consits setuid of next level user which can be used to print the password containing file in the /etc/bandit_pass directory

### Explaination

- The shell file used for the current level uses a the ```more text.txt``` execution and exits after thexecution
- By minimizing/reducing the size of the terminal the more command would not be executed completely
- By pressing ```v``` key, it opens vim and allows user to manipulate the shell by pressing ```:``` and adding the above
- The password was easily found after understanding how to execute the setuid 
