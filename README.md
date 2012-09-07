INTRODUCTION
============
Blowfish is a symmetric-key block cipher designed by Bruce Schneier in 1993. It uses a variable
key length and valid keys have between 32- and 448-bits. He marketed it as a replacement for
DES and IDEA that could be immediately dropped-in. Blowfish is license and patent free for any
use.

Takes a single command line argument of the key in hex [16 hex characters].  It then reads the message as ASCII characters from standard input until end-of-file on standard input.
Each block is 8 characters [64 bits] split into 2 32-bit pieces
L0 and R0; the final block is to be extended with bytes of 0
[the C character ’\0’] if needed. The output is to be printed
to the screen as hexadecimal bytes. The encryption relies on 2
operations: addition mod 232 [written +] and XOR [written ].
The i-th round takes 2 32-bit inputs Li−1 and Ri−1 and 1 32-bit
subkey Pi and produces outputs Li and Ri by (1) generating
Ri = Li−1Pi and (2) Li = F(Ri)Ri−1. The encryption does
16 rounds, then L17 = R16  P18 and R17 = L16  P17.
The function F(x) relies on 4 S-boxes, each of which contains
256 entries, one for each possible byte. Split x into 4 bytes: a,
b, c, and d. Then F(x) = ((S1(a) + S2(b))  S3(c)) + S4(d).
The hard part of Blowfish, and the part that makes it secure,
is the subkey and S-box generation; both depend on the initial key.  The input key is divided into 32-bit pieces: K1 and K2.
Initialize the subkeys and the S-boxes to the fractional part of
 in the order P1 through P4, then S1(0) through S1(255), then all of S2, S3, and S4. Then compute Pi = Pi  K1 for odd i and Pi = Pi  K2 for even i. Now encrypt a 64-bit block of zeros with these P and S to get new P1 [left half] and P2. Then encrypt that answer [P1||P2]
with the new P and S to get new P3 and P4. Then continue this
process to update the P and S arrays in the order above [first
all the P, then all the S1, S2, S3, and S4. Now you are ready to
do the real encryption. Notice that this takes a lot of time; this
is NOT a good encryption scheme if the key changes frequently.

USE
===
==> blow [16 hex key]
Enter Message Here: Hello World
[Ciphertext displayed here]
