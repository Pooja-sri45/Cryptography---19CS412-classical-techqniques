# Cryptography---19CS412-classical-techqniques
# NAME: POOJASRI L
# REG.NO:212223220076

# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
void main()
{
    char plain[10],cipher[10];
    int key,i,length;
    int result;
    printf("\n ENTER THE PLAIN TEXT: ");
    scanf("%s", plain);
    printf("\n ENTER THE KEY VALUE: ");
    scanf("%d", &key);
    printf("\n \n \t PLAIN TEXT: %s", plain);
    printf("\n \n \t ENCRYPTED TEXT: ");
    for(i=0, length = strlen(plain); i<length; i++)
    {
        cipher[i]=plain[i] + key;
        if (isupper(plain[i]) && (cipher[i] > 'Z'))
        cipher[i] = cipher[i] - 26;
        if (islower(plain[i]) && (cipher[i] > 'z'))
        cipher[i] = cipher[i] - 26;
        printf("%c", cipher[i]);
    }
    printf("\n \n \t AFTER DECRYPTION : ");
    for(i=0;i<length;i++)
    {  
        plain[i]=cipher[i]-key;
        if(isupper(cipher[i])&&(plain[i]<'A'))
        plain[i]=plain[i]+26;
        if(islower(cipher[i])&&(plain[i]<'a'))
        plain[i]=plain[i]+26;
        printf("%c",plain[i]);
    }
    getchar(); 
}
```

## OUTPUT:
![Screenshot 2025-03-19 135434](https://github.com/user-attachments/assets/6d32b441-631f-43fe-98e6-8614abefc62e)

## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#define SIZE 5
char keyMatrix[SIZE][SIZE] = {
{'M', 'O', 'N', 'A', 'R'},
{'C', 'H', 'Y', 'B', 'D'},
{'E', 'F', 'G', 'J', 'K'},
{'L', 'P', 'Q', 'S', 'T'},
{'U', 'V', 'W', 'X', 'Z'}
};
void findPosition(char ch, int *row, int *col) {
for (int i = 0; i < SIZE; i++) {
for (int j = 0; j < SIZE; j++) {
if (keyMatrix[i][j] == ch) {
*row = i;
*col = j;
return;
}
}
}
}
void playfairCipher(char text[], char result[], int encrypt) {
int row1, col1, row2, col2, shift = encrypt ? 1 : -1;
int len = strlen(text);
for (int i = 0; i < len; i += 2) {
findPosition(text[i], &row1, &col1);
findPosition(text[i + 1], &row2, &col2);
if (row1 == row2) {
result[i] = keyMatrix[row1][(col1 + shift + SIZE) % SIZE];
result[i + 1] = keyMatrix[row2][(col2 + shift + SIZE) % SIZE];
} else if (col1 == col2) {
result[i] = keyMatrix[(row1 + shift + SIZE) % SIZE][col1];
result[i + 1] = keyMatrix[(row2 + shift + SIZE) % SIZE][col2];
} else {
result[i] = keyMatrix[row1][col2];
result[i + 1] = keyMatrix[row2][col1];
}
}
result[len] = '\0';
}
int main() {
char plaintext[] = "POOJASHREE";
char encryptedText[100], decryptedText[100];
playfairCipher(plaintext, encryptedText, 1);
printf("Encrypted Text: %s\n", encryptedText);
playfairCipher(encryptedText, decryptedText, 0);
printf("Decrypted Text: %s\n", decryptedText);
return 0;
}
```
## OUTPUT:
![Screenshot 2025-03-16 211242](https://github.com/user-attachments/assets/29e2b064-2efe-4a8d-a9b1-a39760f03d10)


## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.


## PROGRAM: 
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>
#define SIZE 2
int keyMatrix[SIZE][SIZE] = {{3, 3}, {2, 5}};
int modInverse(int a, int m) {
a = a % m;
for (int x = 1; x < m; x++)
if ((a * x) % m == 1)
return x;
return -1;
}
int determinant(int matrix[SIZE][SIZE]) {
return (matrix[0][0] * matrix[1][1] - matrix[0][1] * matrix[1][0]) % 26;
}
void inverseMatrix(int matrix[SIZE][SIZE], int invMatrix[SIZE][SIZE]) {
int det = determinant(matrix);
if (det < 0) det += 26;
int detInv = modInverse(det, 26);
if (detInv == -1) {
printf("Inverse does not exist!\n");
exit(0);
}
invMatrix[0][0] = matrix[1][1] * detInv % 26;
invMatrix[0][1] = -matrix[0][1] * detInv % 26;
invMatrix[1][0] = -matrix[1][0] * detInv % 26;
invMatrix[1][1] = matrix[0][0] * detInv % 26;
for (int i = 0; i < SIZE; i++)
for (int j = 0; j < SIZE; j++)
if (invMatrix[i][j] < 0)
invMatrix[i][j] += 26;
}
void matrixMultiply(int matrix[SIZE][SIZE], int message[], int result[]) {
for (int i = 0; i < SIZE; i++) {
result[i] = 0;
for (int j = 0; j < SIZE; j++)
result[i] += matrix[i][j] * message[j];
result[i] %= 26;
}
}
void encryptMessage(char message[], char encrypted[]) {
int messageVector[SIZE], cipherVector[SIZE];
int len = strlen(message);
if (len % SIZE != 0) {
strcat(message, "X");
len++;
}
for (int i = 0; i < len; i += SIZE) {
for (int j = 0; j < SIZE; j++)
messageVector[j] = toupper(message[i + j]) - 'A';
matrixMultiply(keyMatrix, messageVector, cipherVector);
for (int j = 0; j < SIZE; j++)
encrypted[i + j] = cipherVector[j] + 'A';
}
encrypted[len] = '\0';
}
void decryptMessage(char encrypted[], char decrypted[]) {
int invKeyMatrix[SIZE][SIZE];
inverseMatrix(keyMatrix, invKeyMatrix);
int cipherVector[SIZE], messageVector[SIZE];
int len = strlen(encrypted);
for (int i = 0; i < len; i += SIZE) {
for (int j = 0; j < SIZE; j++)
cipherVector[j] = encrypted[i + j] - 'A';
matrixMultiply(invKeyMatrix, cipherVector, messageVector);
for (int j = 0; j < SIZE; j++)
decrypted[i + j] = messageVector[j] + 'A';
}
decrypted[len] = '\0';
}
int main() {
char message[100] = "POOJASRI";
char encrypted[100], decrypted[100];
encryptMessage(message, encrypted);
printf("Encrypted Message: %s\n", encrypted);
decryptMessage(encrypted, decrypted);
printf("Decrypted Message: %s\n", decrypted);
return 0;

```
## OUTPUT:
![Screenshot 2025-03-17 120526](https://github.com/user-attachments/assets/d89ae389-c208-4f9b-bc81-8a3d670d20e5)


## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



## PROGRAM:
```
#include <stdio.h>
#include <string.h>
void vigenereEncrypt(char text[], const char key[]) {
int textLen = strlen(text);
int keyLen = strlen(key);
for (int i = 0; i < textLen; i++) {
char c = text[i];
if (c >= 'A' && c <= 'Z') {
text[i] = ((c - 'A' + key[i % keyLen] - 'A') % 26) + 'A';
} else if (c >= 'a' && c <= 'z') {
text[i] = ((c - 'a' + key[i % keyLen] - 'A') % 26) + 'a';
}
}
}
void vigenereDecrypt(char text[], const char key[]) {
int textLen = strlen(text);
int keyLen = strlen(key);
for (int i = 0; i < textLen; i++) {
char c = text[i];
if (c >= 'A' && c <= 'Z') {
text[i] = ((c - 'A' - (key[i % keyLen] - 'A') + 26) % 26) + 'A';
} else if (c >= 'a' && c <= 'z') {
text[i] = ((c - 'a' - (key[i % keyLen] - 'A') + 26) % 26) + 'a';
}
}
}
int main() {
const char *key = "KEY";
char message[] = "ImPoojaSri";
printf("\nInput Message : %s\n", message);
vigenereEncrypt(message, key);
printf("Encrypted Message: %s\n", message);
vigenereDecrypt(message, key);
printf("Decrypted Message: %s\n", message);
return 0;
}
```
## OUTPUT:
![Screenshot 2025-03-17 162037](https://github.com/user-attachments/assets/ad76dfb2-a24c-4ead-901a-72d4a73722f2)

## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:
```
#include <stdio.h>
#include <string.h>
void encrypt(char str[], int rails);
void decrypt(char str[], int rails);
int main() {
 int rails;
 char str[1000];
 printf("Enter a message: ");
 fgets(str, sizeof(str), stdin);
 str[strcspn(str, "\n")] = '\0';
 printf("Enter number of rails: ");
 scanf("%d", &rails);
 getchar();
 encrypt(str, rails);
 decrypt(str, rails);
 return 0;
}
void encrypt(char str[], int rails) {
 int len = strlen(str);
 char rail[rails][len];
 for (int i = 0; i < rails; i++)
 for (int j = 0; j < len; j++)
 rail[i][j] = '\n';
 int row = 0, down = 1;
 for (int i = 0; i < len; i++) {
 rail[row][i] = str[i];
 if (row == rails - 1)
 down = 0;
 else if (row == 0)
 down = 1;
 row += down ? 1 : -1;
 }
 printf("Encrypted message: ");
 for (int i = 0; i < rails; i++)
 for (int j = 0; j < len; j++)
 if (rail[i][j] != '\n')
 printf("%c", rail[i][j]);
 printf("\n");
}
void decrypt(char str[], int rails) {
 int len = strlen(str);
 char rail[rails][len];
 for (int i = 0; i < rails; i++)
 for (int j = 0; j < len; j++)
 rail[i][j] = '\n';
 int row = 0, down = 1;
 for (int i = 0; i < len; i++) {
 rail[row][i] = '*';
 if (row == rails - 1)
 down = 0;
 else if (row == 0)
 down = 1;
 row += down ? 1 : -1;
 }
 int index = 0;
 for (int i = 0; i < rails; i++)
 for (int j = 0; j < len; j++)
 if (rail[i][j] == '*' && index < len)
 rail[i][j] = str[index++];
 printf("Decrypted message: ");
 row = 0, down = 1;
 for (int i = 0; i < len; i++) {
 printf("%c", rail[row][i]);
 if (row == rails - 1)
 down = 0;
 else if (row == 0)
 down = 1;
 row += down ? 1 : -1;
 }
 printf("\n");
}

```


## OUTPUT:
![Screenshot 2025-03-17 204907](https://github.com/user-attachments/assets/430c4780-b298-4834-a35c-1e43813b70b2)


## RESULT:
The program is executed successfully
