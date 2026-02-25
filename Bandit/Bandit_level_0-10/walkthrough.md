# Walkthrough for level 0 to 10

method to connect: ssh banditX@bandit.labs.overthewire.org -p 2220

X stands for level number

## Level 0

- use password bandit0 
- readme file would be avalable in the home directory. Use the 'cat' command to display the contents of the file [password is stored in this file]
``` 
cat <file-name>
```

- cat command is used for displaying contents of file and also used for manipulation of file content.

## Level 1

- Password is stored in a file called -
- cat cannot be directly used here, instead use cat ~/- [~ represents home directory]
- ~/- represents the full path of the file -

### Explaination

- cat - cannot be used to display content of the file - because - is used for passing arguements.

## Level 2

- Password is stored in a file called  --spaces in this filename--
- There are 2 ways to use the cat command here:
```
cat ~/--spaces\ in\ this\ filename--
```
OR

```
cat ~/"--spaces in this filename--" 
```
### Explaination

- \ is used as an escaping character, telling the system to ignore the space.
- " " is used to enclose the entire filename, which more convenient method.

## Level 3

- Password is stored in a hidden file in the inhere directory.
- use cd command to change directory.
```
cd <directory-name>
```
- use the ls command with -a to show all the files, folders inside the directory[ including the hidden ones]
```
ls -a
```
-  use the cat command and include the . in front of the filename to display the content of the file.

### Explaination

- when . is used in front the filename, ie .filename that file is hidden/invisble and is not displayed in the file manager by deafualt and will not be shown after using ls command.

## Level 4

- Password is stored in the only human-readable file in the inhere directory
- Use cd to change directory, use ls to show files in the directory.
- The file names of all the file starts with - and only difference in the filename is the last number at the end. making a pattern. [ -file0* ]
- Use the ```file``` command to determine the file type, ie
``` 
file ./-file0* | grep 'ASCII text'
```
- use cat command to display the content of the file which is displayed after the execution of the above command.

### Explaination

-```./-file0*``` means all files inside current directory [ . ] with the name starting with -file0.
- ```|```, this is called a pipe function, here it takes the output of the file command and uses as input for the grep command.
- ```grep 'ASCII text'``` provides the output of the file command with matches the pattern 'ASCII text' [ Human Readable ]

## Level 5

- Password is stored in file with following properties:
    1. Human-readable
    2. 1033 bytes in size
    3. not executable
- Use cd to move directory and use ls to list the content of the directory.
- Use the ```find``` command to find the file with these specific properties.
```
find . -type f -size 1033c !-executable
```
- Use the cat command to display the content of the file which is displayed after executing the above command.

### Explaination

- In the above command:
    - ```.```: to search only within the current directory
    - ```-type f``` : only files [ not directories ]
    - ```-size 1033c``` : file with size of 1033 bytes
    - ```! -executable```: non executable files 
- Using the above arguements the find command finds the file with these properties

## Level 6

- Password is stored in the file somewhere on the server and has the following properties
    1. Owned by user bandit7
    2. Owned by group bandit6
    3. 33 bytes in size
- use the ```find``` as before with different arguements
```
find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null

```

### Explaination

- In the above command;
    -```-type f```: only files [ not directories ]
    - ```-user bandit7```: file with user ownership bandit7
    - ```-group bandit6```: file with group ownership bandit6
    -```-size 33c```: file with size 33 bytes

## Level 7

- Password is stored in the file data.txt next to the word millionth
- Use ls to list the content of the directory [ to check if the file is present in the home directory ]
- Use the command
```
cat <file-name> | grep millionth
```

### Explaination

- The output of ```cat filename ``` is used as input by using the pipe function ```|``` which gives the input to ```grep```
- ```grep``` is used for pattern matching, here grep uses the pattern/word millionth and returns the line containing it.

## Level 8

- Password is stored in the file data.txt and is in the line which occur only once
- Use ls to list the content of the directory [ to check if the file is present in the home directory ]
- Use the command
```
sort <file-name> | uniq -u
```

### Explaination

- ```sort <file-name>``` command reads the content of the file and prints the lines in an alphabetical order
- ```| uniq -u``` takes the output of the ```sort``` command and filters repeated line and shows one instance of the values present [ -u prints only line which is only present once in the file ] 

## Level 9

- Password is stored in the file data.txt and is in one of the human readable lines followed by several "="
- Use ls to list the content of the directory [ to check if the file is present in the home directory ]
- use the command
```
strings data.txt | grep "="
```

### Explaination

- ```strings <file-name>``` is used for displaying only the human readable values in a file
- ```| grep "="``` takes the output of ```strings``` command and uses as the input, searches for lines with "=" in it.

## Level 10

- Password is stored in the file data.txt, which contains base64 encoded data 
- Use ls to list the content of the directory [ to check if the file is present in the home directory ]
- use the command
```
cat <file-name> | base64 -d
```

### Explaination
- ```cat <file-name>``` is used for displaying the content of the file
- ```| base64 -d``` takes the output of ```cat``` command and decodes the base64 encoded text. This is available in nearly all major Linux distros.

