*Crypto Browserify*

Hi I'm Calvin

*Disclaimer*

DOING ANY SORT OF CRYTO IN A REGULAR BROWSER SITE LOADED OVER HTTP WILL END IN TEARS

*Cordova* and *NW.JS* are another matter

also with *CSP*, *HTTPS* and  *App Cache* you come up with something usable

*We Begin*

All of cryptography was divided into three parts

well not really, we're just going to 3 of them

*Encryption* aka *Confidentiality*

How do you make sure no one can else read your message

Is somewhat pointless without

*Authentication*

How do you make sure your message is from who you think it is

The best cipher isn't going to help you if there is a man in the middle decrypting your traffic, reading it, and then re-encrypting it.

*Secret Key Exchange*

How do you securely come up with a key to use to encrypt the message.

If you have some out of band method for doing it...

Why don't you just use that for the message?

*Public Key Exchange*

Will not be covered, that's more of a social issue.

Plus node doesn't have it.

*Background on node crypto*

Think layer around openssl

yes that openssl

node relies on some poorly documented features

*yay*

*Encryption*

Only modern cipher Node (openssl) implements is AES

16/24/32byte *key* + 16byte *plaintext* = 16byte *ciphertext*

This is useless by itself

*Mode Of Operation*

16/24/32byte *key* + 16/12byte *IV/NONCE* + anysize *plaintext* = anysize *ciphertext*

*CBC*

16 bit IV

block 1: enc(plain text xor iv) = ciphertext 1

block 2: enc(plain text xor ciphertext 1) = ciphertext 2

simple

NOT SECURE DON'T USE

enc(plainText-n xor CipherText-(n-1) xor lastCipherText) = cipherText-n

or

does this decrypt to that

*CTR*

16 bit IV

block 1: enc(iv) xor plain text 1 = ciphertext 1

block 2: enc(iv + 1) xor plain text 2 = ciphertext 2
