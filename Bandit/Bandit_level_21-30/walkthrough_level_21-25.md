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
- The content of the executable mentioned in the ```/etc/cron.d/<file-name>```
```
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

```
- Check the /tmp file to check the password of the next level

### Explaination

- To find the name of the file, execute the command ```echo I am user $myname | md5sum | cut -d ' ' -f 1``` 
- Replace the $myname variable with the username of the next level and use the resulting value, along with /tmp to find the file with password of the next level.

## Level 23

- The same as method used in level 21, find the executable mentioned in the ```/etc/cron.d/<file-name>``` and understand what happens when the file is executed.
- The content of the exectuable used for the cron job:
```
#!/bin/bash
shopt -s nullglob
myname=$(whoami)

cd /var/spool/"$myname"/foo || exit 
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done
```
- Use the ```mktemp -d``` to create a temporary directory in the ```/tmp``` directory. Also create a file to store the password.
```
touch <file-name>
chmod 777 <file-name>
```
- Create a script to copy the password of the next level to the file created in the temporary directory
```
#!/bin/bash
cat /etc/bandit_pass/<file-name> > /temporary directory/<file-name>
```
- Also change the permissions of the script file using ```chmod``` to make it as an executabe.
- Copy this script file to the directory mentioned in the executable of the cronjob.
- After some times, use the ```cat``` command to show the password which is added to the file.

### Explaination

- The executable used in the cronjob reads the content of the directory /var/spool/<username>/foo and executes the files inside that directory. After execution the file is deleted.
- So the logic here is to create a script which will be added to the directory mentioned above. The script will be used to reveal the password of the next level. 
