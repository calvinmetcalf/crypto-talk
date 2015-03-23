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

block 1: enc( *plain text* xor *iv* ) = *ciphertext 1*

block 2: enc( *plain text* xor *ciphertext 1* ) = *ciphertext 2*

NOT SECURE DON'T USE

enc( *plainText-n* xor *CipherText-(n-1)* xor *lastCipherText* ) = *cipherText-n*

or

does this decrypt to that

*CTR*

16 bit IV

block 1: enc( *iv* ++) xor *plain text 1* = *ciphertext 1*

block 2: enc( *iv* ++) xor *plain text 2* = *ciphertext 2*

*GCM* variant

12 bit IV

block 1: enc( *iv* concat 0001) xor *plain text 1* = *ciphertext 1*

block 2: enc( *iv* concat 0002) xor *plain text 2* = *ciphertext 2*

*Secret Key Exchange*

Requires *Big Numbers* or *Elliptical Curves*

*Fedor* did the hard word for me

Modulo is just like normal except with division

*Diffie-Hellman*

pick a large prime

like really large

and pick a base (like 2, some restrictions, kinda complex)

these are agreed upon before hand

pick a large integer 

calculate *base* ^ *integer* mod *prime*

send that to friend

friend has done the same thing with a diff integer

then you both go

*thing they sent me* ^ *my integer* mod *prime*

we get the same number

the whole modpow thing is tricky

huge performance differences

if base is *2*

and integer is *26971*

*2* ^ *26971* = *8120* digit number

*RSA*

Also uses big numbers

you have a *public* and *private* key

things encrypted with one can be encrypted by the other

but can't decrypt things encrypted with the same key

so pick random number

use it to encrypt message

encrypt random number with person's public key

send encrypted key and encrypted message

with *RSA* someone steals key can decrypt all old messages

not so with *diffie-hellman*

*Authentication*

Building block: *hash*

put stuff in, get fixed length stuff out

put in every so slightly different stuff in, get very different stuff out

*HMAC*

~HASH( *message* + *key* ) but better

still need to send hmac key

but can do something simple like

"before encrypting anything encrypt 32 bytes of zeros"

*Authenticated Encryption*

AKA mode of operation plus mac

2 for 1!

*GCM*

Modified counter mode (good)

*GHASH* function (terrible)

only one in node crypto lib

(though chacha20/poly1305 is a different good one)

*Public Key Signatures*

*RSA*

take hash of message

encrypt with *private* key

*DSA*

1. pick a random number

2. are you sure it's random?

3. because if you ever repeat it, your key is leaked

4. hope the NSA didn't back door any PRNGs

or do what openssl (and node) don't do

hmac( *private key*, *message* ) = will always be different

*Eliptical Curves*

Imagine integers but in 2 dimmentions

or something I got no idea

*Conclution*

you're going to get hacked
