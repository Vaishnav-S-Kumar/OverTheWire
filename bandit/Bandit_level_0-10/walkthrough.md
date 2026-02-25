# Walkthrough for level 0 to 10

method to connect: ssh banditX@bandit.labs.overthewire.org -p 2220

X stands for level number

## Level 0

- use password bandit0 
- readme file would be avalable in the home directory. Use the 'cat' command to display the contents of the file [password is stored in this file]
``` 
cat <file-name>
```

- cat command is used for displaying contents of file and also used for manipulation of file content

## Level 1

- Password is stored in a file called -
- cat cannot be directly used here, instead use cat ~/- [~ represents home directory]
- ~/- represents the full path of the file -.

### Why
- cat - cannot be used to display content of the file - because - is used for passing arguements

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
### Why
- \ is used as an escaping character, telling the system to ignore the space
- " " is used to enclose the entire filename, which more convenient method

## Level 3

- Password is stored in a hidden file in the inhere directory
- use cd command to change directory
```
cd <directory-name>
```
- use the ls command with -a to show all the files, folders inside the directory[ including the hidden ones]
```
ls -a
```
-  use the cat command and include the . in front of the filename to display the content of the file

### Why
- when . is used in front the filename, ie .filename that file is hidden/invisble and is not displayed in the file manager by deafualt and will not be shown after using ls command

## Level 4

- Password is stored in the only human-readable file in the inhere directory
- Use cd to change directory, use ls to show files in the directory.
- The file names of all the file starts with - and only difference in the filename is the last number at the end. making a pattern. [ -file0* ]
- Use the ```file``` command to determine the file type, ie
``` 
file ./-file0* | grep 'ASCII text'
```
- use cat command to display the content of the file which is displayed after the execution of the above command

### Why
-``` ./-file0*``` means all files inside current directory [ . ] with the name starting with -file0
- ```|```, this is called a pipe function, here it takes the output of the file command and uses as input for the grep command
- ```grep 'ASCII text'``` provides the output of the file command with matches the pattern 'ASCII text' [ Human Readable ]
