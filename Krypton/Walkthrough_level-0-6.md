# Walkthrough for level 0 to 7

Format for SSH login or access to each level

```
ssh kryptonX@krypton.labs.overthewire.org -p 2231
```
The X stands for level number, Which level you are going to access

## Level 0 

- To access the first level, decode the the string given in the level description. The string is base64 enoded. 
- To decode the given string, use the following command
```
echo <string> | base64 -d
```
- After decoding, log into the first level using SSH format given above.

## Level 1


