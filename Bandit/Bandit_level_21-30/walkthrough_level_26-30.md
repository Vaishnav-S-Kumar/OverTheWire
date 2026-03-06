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

## Level 27

- Password for the next level can be found in a git repositery at ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo via the port 2220.
- Instead of SSH into the Level, use your local machine and use the ```git clone``` command:
```
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```
- Use ```cd``` to change directory to repo and use ```cat``` to print the contents of the file

### Explaination

- Without using the port number, the repositery cannot be cloned and the result will be a error message- To use the port number, enter it at the end of the hostname as an extenstion instead of using a flag like ```-p``` or ```-P```

## Level 28

- Same as in the previous levels, Clone the git repositery mentioned in the description and use the same command format as in the previous level.
- After cloning the database, use ```cd``` to change the directory and use ```cat``` to show the contents of the file
```
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx

```
- As seen above the password is changed, to find the password use the command 
```
git log
```
- Copy the commit hash which shall give us the password or commit hash which is before the commit which changes the password. Use the command 
```
git checkout <commit-hash>
```
- Use the ```cat``` command to read the content of the file 

### Explaination

- The ```git log``` command gives the full history of the repositery and what all changes has been made.
- The ```git checkout``` command reverts the changes back to the commit whose commit hash is used alongside this command.
