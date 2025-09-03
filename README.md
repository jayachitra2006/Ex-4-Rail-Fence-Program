# Ex-5 Rail-Fence-Program
Name : jayachitra J
Reg : 212224040132

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
~~~
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
void encryptRailFence(char str[], int rails, char encrypted[]) {
int i, j, len, count, code[100][1000];
len = strlen(str);
// Initialize the code array to 0
for (i = 0; i < rails; i++) {
for (j = 0; j < len; j++) {
code[i][j] = 0;
}
}
count = 0;
j = 0;
while (j < len) {
if (count % 2 == 0) { // Moving down the rails
for (i = 0; i < rails && j < len; i++) {
code[i][j] = (int)str[j];
j++;
}

} else { // Moving up the rails
for (i = rails - 2; i > 0 && j < len; i--) {
code[i][j] = (int)str[j];
j++;
}
}
count++;
}

int pos = 0;
for (i = 0; i < rails; i++) {
for (j = 0; j < len; j++) {
if (code[i][j] != 0) {
encrypted[pos++] = code[i][j];
}
}
}
encrypted[pos] = '\0'; // Null-terminate the string
}
void decryptRailFence(char str[], int rails, char decrypted[]) {
int i, j, len, count, code[100][1000], pos = 0;
len = strlen(str);
// Initialize the code array to 0
for (i = 0; i < rails; i++) {
for (j = 0; j < len; j++) {
code[i][j] = 0;
}
}
// Mark the positions where characters will go
count = 0;
j = 0;
while (j < len) {
if (count % 2 == 0) { // Moving down the rails
for (i = 0; i < rails && j < len; i++) {
code[i][j] = 1;
j++;
}
} else { // Moving up the rails
for (i = rails - 2; i > 0 && j < len; i--) {
code[i][j] = 1;
j++;
}
}
count++;
}
// Fill the marked positions with the characters from the cipher text
for (i = 0; i < rails; i++) {
for (j = 0; j < len; j++) {
if (code[i][j] == 1) {
code[i][j] = str[pos++];
}
}
}
// Reconstruct the decrypted message by following the zigzag pattern
pos = 0;
count = 0;
j = 0;
while (j < len) {
if (count % 2 == 0) { // Moving down the rails
for (i = 0; i < rails && j < len; i++) {
if (code[i][j] != 0) {
decrypted[pos++] = code[i][j];
}
j++;
}
} else { // Moving up the rails
for (i = rails - 2; i > 0 && j < len; i--) {
if (code[i][j] != 0) {
decrypted[pos++] = code[i][j];
}
j++;
}
}
count++;
}
decrypted[pos] = '\0'; // Null-terminate the string
}
int main() {
char str[1000], encrypted[1000], decrypted[1000];
int rails;
printf("Simulating Rail Fence Cipher\n");
printf("Enter a Secret Message: ");
fgets(str, sizeof(str), stdin);
str[strcspn(str, "\n")] = 0; // Remove trailing newline character if exists

printf("Enter number of rails: ");
scanf("%d", &rails);
// Encrypt the message
encryptRailFence(str, rails, encrypted);
printf("Encrypted Message: %s\n", encrypted);
// Decrypt the message
decryptRailFence(encrypted, rails, decrypted);
printf("Decrypted Message: %s\n", decrypted);
return 0;
}
~~~



# OUTPUT
<img width="1746" height="923" alt="Screenshot 2025-09-03 090252" src="https://github.com/user-attachments/assets/60bdeed3-9e85-4459-97d2-8854ceddb492" />


# RESULT
this program is executed successfully
