*Crypto Browserify*

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
