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

## Level 2

- Password for the next level is in the file krypton3 which is encrypted using caesar cipher. One feature about ceasar cipher is the number of the characters to shift can vary.
- It is also mentioned the characters changes the case, ie lowercase is converted to uppercase
- There are additional information provided which describes how the file has been encrypted, ie
    - A binary is available in the directory which is stored in the same directory where krypton3 is stored. The binary is called encrypt, so this binary would have used to encypt the content of krypton3.
    - The binary uses keyfile which is available in the directory where it is used and encrypts the file
- The following steps can used for getting the password:
    1. Create and shift the operation to temporary directory
    ```
    cd $(mktemp -d)
    ```
    2. Create a link to the keyfile which is stored in the directory where krypton3 is stored. So that binary could access the keyfile which is used for encrypting krypton3 
     ```
    ln -s <file>
    ```
    3. change the permissions of the file using ```chmod```
    ```
    chmod 777 .
    ```
    4. Execute the binary along with file containing the following ```abcdefg```
    ```
    ./<binary-name> <file>
    ```
    5. A new file would be created in the directory with name ```ciphertext``` and analyse the pattern of the text in the file ```ciphertext```. After analysis create the pattern sets <set-1> <set-2>
    ```
    cat ciphertext | tr <set-1> <set-2> 
    ```
    
