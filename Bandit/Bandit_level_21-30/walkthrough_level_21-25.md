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

