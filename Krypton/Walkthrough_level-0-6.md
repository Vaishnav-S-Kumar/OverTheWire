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
## Level 3   

- Password is found in file called krypton4, The directory also contains 6 more files called found1, found2, found3 along with files HINT1, HINT2 and README
- The password is encypted using a substitution cipher but this time the mechanism used is not given. To find the mechanism used, analyse the file found1, found2 and found3 since it is also encrypted using the same method.
- Upon opening the files HINT1 and HINT2, we get the following hints
```
Some letters are more prevalent in English than others.
"Frequency Analysis" is your friend.
```

- The first hint points out that some letters in the english alphabets are occuring more than others. Basically it means to find the alphabet in the cipher texts that occur the most and replace it with the alphabet which is used most in english. 
- Use google to learn more on frequency analysis and understand the concept 
- First, the number of occurence of each character should be calculated, i.e using the follwing
```
for i in {A..Z}; do cat found*|tr -cd $i| wc -c| tr -d "\n"; printf " $i \n"; done | sort -nr
```
- The result for the above command would be
```
<Number of occurence> <Alphabet> 
```
- Arrange the result of the above command in a single line format for example ```THYFJSIMAPQWERY...``` 
- Use google or chatgpt to find the list of alphabets that occur most till the one which occur least. for example it would be like ```ETAOINSHRDLUCMWYFGPBVKJXQ```
- Use ```cat``` and ```tr``` command to replace the letters of the file, i.e
```
cat <file-name> | tr <result-set> <occurence-set>
```
- Change the occurence-set until and unless a clear message appears.

## Level 4

- Password is stored in the file krypton5, the content of the file is encrypted using Vignère Cipher. It is encrypted using a 6 letter key. The other files in the directory of krypton5 is HINT, found1 and found2 along with a README file describing the level.
```
Good job!

You more than likely used frequency analysis and some common sense
to solve that one.

So far we have worked with simple substitution ciphers.  They have
also been 'monoalphabetic', meaning using a fixed key, and
giving a one to one mapping of plaintext (P) to ciphertext (C).
Another type of substitution cipher is referred to as 'polyalphabetic',
where one character of P may map to many, or all, possible ciphertext
characters.

An example of a polyalphabetic cipher is called a Vigen�re Cipher.  It works
like this:

If we use the key(K)  'GOLD', and P = PROCEED MEETING AS AGREED, then "add"
P to K, we get C.  When adding, if we exceed 25, then we roll to 0 (modulo 26).


P     P R O C E   E D M E E   T I N G A   S A G R E   E D
K     G O L D G   O L D G O   L D G O L   D G O L D   G O

becomes:

P     15 17 14 2  4  4  3 12  4 4  19  8 13 6  0  18 0  6 17 4 4   3
K     6  14 11 3  6 14 11  3  6 14 11  3  6 14 11  3 6 14 11 3 6  14
C     21 5  25 5 10 18 14 15 10 18  4 11 19 20 11 21 6 20  2 8 10 17

So, we get a ciphertext of:

VFZFK SOPKS ELTUL VGUCH KR

This level is a Vigen�re Cipher.  You have intercepted two longer, english
language messages.  You also have a key piece of information.  You know the
key length!

For this exercise, the key length is 6.  The password to level five is in the usual
place, encrypted with the 6 letter key.

Have fun!
```
- This level can be solved using two methods and both does not include the terminal.One method using the website DeCode.fr and Other is using some simple calculations.
- Even though we are using the website, some additonal information can narrow the search. Start by opening both the found files. Notice that both the file starts with YYI which could mean THE.- Keeping that in mind calculate the KEY 
```
YYI     24 24 8 (Cipher)
THE     19  7 4 (Plain)

FRE      5 17 4 (Key)
```
- Using this information, go to DeCode.fr and paste the content of found1. Use the ```Knowing only a partial key (joker=?):``` and enter the Key and decrypt.
- After that use second option ```Knowing the key-length/size, number of letters:``` and press decrypt. Different number of keys would be used of the size 6. 
- With all the different types of keys, replace the content of found1 with krypton5 and use the option ```Knowing the Key/Password:``` and try those different keys until a proper text is formed

- Second mehod would be to use the key and ciphertext directly to get the palintext.
```
HCIKV RJOX (Cipher)  
FRE.. .FRE (Key)

CLE.. .EXT (Plain)
```
- using chatgpt or any online tool, find the suitable missing letters

