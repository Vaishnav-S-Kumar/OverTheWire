# Walkthrough for level 11 to 15

method to Access each level: ```ssh banditX@bandit.labs.overthewire.org -p 2220```

X stands for level number

## Level 11

- Password is stored in the file called data.txt, where all letters have been rotated by 13 positions
- Use ls to list the content of the directory [ to check if the file is present in the home directory ]
- use the command
```
cat <file-name> | tr a-zA-Z n-za-mN-ZA-M
```

- second method: use cyberchef and use the algorithm ROT13

### Explaination

- ```cat <file-name>``` is used for displaying the content of the file
- ```tr``` command translate/replace first set to second set ie. In the above example, it will change a to n or b to o
- ```| tr a-zA-Z n-za-mN-ZA-M``` takes the output of ```cat``` command and use it as input for the ```tr``` command 

## Level 12

- Password is stored in the file called data.txt, which is the hexdump of a file that has been repeatedly compressed. 
- What it means is the original file which contains the password is plaintext is compressed repeatedly and then converted into a hexdump
- Use ls to list the content of the directory [ to check if the file is present in the home directory ]
- First, create a diretory in the tmp directory and using it for operations, ``` cd $(mktemp -d)```
- Copy the file to the temporary directory using ```cp ~/<file-name>``` <br>
- The following commands were used retrieving the plaintext password:
    - ```xxd```
    - ```gzip```,```bzip2```,```tar```
    - ```file```
    - ```mv```

### Explaination

- use the man pages and google search to find how to reverse/decompress each methods.
- The method used was to reverese the hexdump into normal compressed file
- ```file``` command was used to identify what type of file it was
- ```mv``` command was to rename the filename with the extension of the file type, ie if file type is POSIX tar archive (GNU), then file should be <file-name>.tar
- After repeating this methods, eventually the file with plain text would be retrieved. the file type would be ASCII text

## Level 13

- Password is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. There is a private SSH key in the home directory to log in to the next level for now.
- To transfer SSH key from bandit to our machine use the command ```scp```, from player machine [ you ].
- use the command
```
scp -P <port-number> bandit13@bandit.labs.overthewire.org:/<file-path> <destination>
```
- Second method would be to SSH login to the machine and manually copy the contents of the file and create a file on player machine and paste the content. <br>

- In both case, use ```chmod``` command to change the permissions of the file so that ssh shall accept it when accessing the next level. **Make it only accessible by the user** 

### Explaination

- ```scp``` stands for Secure Copy Protocol, which is secure method for transfering the files from one machine to another.
- Here, instead of using SSH to access the same credentials is used in scp to tranfer the files to the player machine.

## Level 14

- Password can retrieved by submittinig the password of the current level on port 30000 on localhost
- Use SSH method of using file/SSH key to login into this level, after login use ```cat``` command to read the file mentioned in the last challenge where the password is stored.
- use the command 
```
telnet <host> <port>
```
- Submit the password of this level and wait

### Explaination
- telnet is a network protocol with allows to connect to and communicate with remote computers over TCP/IP.
- Here, the password is entered to the terminal using telnet. The service on that port verifies the password and returns the password of the next level.

## Level 15

- Password can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.
- Use the command
```
openssl s_client -connect <host>:<port>
```
- Submit the password of the current level

### Explaination

- ```openssl``` is a toolkit which is used to implement SSL/TLS protocol for various pruposes such as creation of keys, establishing connection, etc. 
- The above command is used to establish a connection to server [ <host>:<port> ] as a client using SSL/TLS encryption protocol
