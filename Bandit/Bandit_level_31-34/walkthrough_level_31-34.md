# Walkthrough for level 31 to 34

method to Access each level: ```ssh banditX@bandit.labs.overthewire.org -p 2220```

X stands for level number

## Level 31

- Password is stored in a github repositery, Same as in the previous level. Clone the repositery mentioned in description using the technique used before.
- After cloning, use ```cd <directory-name>``` and use ```cat <file-name>``` to show the contents of the file present in the directory. 
```
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```
- So, as described we are required to create a .txt file and upload it to this repository. Use the following command:
```
echo <content> >> <file-name>
git add <file-name>
```
- We get the following printed in the terminal after executing the last command
```
The following paths are ignored by one of your .gitignore files:
key.txt
hint: Use -f if you really want to add them.
hint: Disable this message with "git config set advice.addIgnoredFile false"
```
- We can add the file by two ways:
    - Editing the .gitignore and removing the configuration which does not allow adding the file
    - We can use -f with git add 
- After adding the file, commit command is executed with description
```
git commit -m <description/message>
```
- At last the file is uploaded to repositery using the command
```
git push -u origin <branch-name>
```

### Explaination 
- .gitignore is a file which tells git to ignore certain types of file when the user tries to upload it.
- Changing the configuration/or content can modify the behaviour of git to certain files.
- -f is used to forcefully upload the file to the index,
- The commit message is let the user understand what has been changed or modified.
- At last the push command, pushes the changes to repositery under the mentioned branch.
