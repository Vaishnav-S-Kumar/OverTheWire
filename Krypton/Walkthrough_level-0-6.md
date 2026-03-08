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

- Password for next level lies in a file called krypton2, it is encrypted using a simple rotation which is a standard ciphertext format.
- From the description, we can assume it is using a ROT13 algorithm to convert the real password to ciphertext.
- Use the ```find``` command to find the file location of krypton2:
```
find / -type f -name <file-name>
``` 
- Here ```-type f``` refers to the type of data ```f``` means file
- Use the following command to decrypt the contain of the file afte finding the location of the file
```
cat <file-location> | tr <first-set> <second-set>
```
- The ```tr``` command translates/replace first set to second set.

