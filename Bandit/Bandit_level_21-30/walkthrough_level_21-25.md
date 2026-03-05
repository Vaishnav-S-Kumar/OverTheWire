# Walkthrough for level 21 to 25

method to Access each level: ```ssh banditX@bandit.labs.overthewire.org -p 2220```

X stands for level number

## Level 21

- Password can be found after understanding the configuration of the cronjob of the next level, i.e by checking the cronjob file in /etc/cron.d/ use the command:
```
cat /etc/cron.d/<file-name>
```

### Explaination

- Understand what file is will do. Here it executes a file at specific time. Read the contents of the file which is to be executed and read the file using ```cat``` and continue the process until the password is printed
- Learn more about what is cronjob and how it is configured

## Level 22

- Same as level 21 password can be found after understanding the configuration of the cronjob of the next level.
- Use the following command to find configuration of the cron job of the next level:
```
cat /etc/cron.d/<file-name>
```
- The content of the executable mentioned in the```/etc/cron.d/<file-name>```
```
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

```
- Check the /tmp file to check the password of the next level

### Explaination

- To find the name of the file, execute the command ```echo I am user $myname | md5sum | cut -d ' ' -f 1``` 
- Replace the $myname variable with the username of the next level and use the resulting value, along with /tmp to find the password of the next level
