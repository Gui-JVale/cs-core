---
sidebar_position: 5
---

# Securing E-Mail

## Introduction

Now that we've seen what end-point authentication is, and how it can be implemented using clever techniques and cryptography, let's take a look at how this gets implemented in practice, adding security to protocols we're already familiar with.

The first one is e-mail which uses SMTP. As we've seen, mail servers talk to each other through the network, which always is exposed to attacks.

So in the same way we went over end-point authentication, let's see how one would design a secure email protocol, and then we'll check out the protocols that are used today for that.

## Designing a Secure E-Mail

What security traits would users exchanging mail through a network want? Well, first thing that comes to mind it's _confidentiality_, so users can have peace of mind that nobody will read the contents of their conversations. Other crucial aspects are _message integrity_, so they know that the contents of their email hasn't been tempered with, and _authentication_, so that they know that the person on the other side is legitimate who they want to talk to. As always, we'll use the example that Alice and Bob want to exchange emails, and the intruder Trudy is trying to intrude and do bad things.

Alright, so let's get to work. As we've seen, to achieve confidentiality we can use **symmetric key encryption** (through AES or DES). The problem with that is the distribution of the key securely, and so the next logic step is to use **public key encryption** (using RSA), but using that is computationally expensive, so in let's get the best of both worlds and use a little bit of both. In practice, it would look something like this:

1. Alice writes an email _m_ to Bob
2. Alice chooses a random _session key_ _K_, and encrypts the email _K(m)_
3. Alice then encrypts _K_ using Bob's public key (that's certified by a CA), and concatenates the encrypted key to the already encrypted email, creating a package that she sends to Bob.
4. Bob, using his private key decrypts the the session key _K_, and uses it to decrypt the email _m_.

Now message integrity and authentication, what are we going to use for those? Hopefully you've guessed it, **cryptographic hash functions**, and **digital signatures**! So let's forget about confidentiality for a bit, and focus on those two aspects:

1. Alice writes an email _m_ to Bob
2. Alice computes the **message digest** using MD5
3. Alice then uses her private key to compute her **digital signature** on the message digest
4. Alice concatenates her digital signature to the original message, creating a package
5. Alice then sends the package to Bob.
6. Bob receiving the package, uses Alice's public key, to decrypt the message digest.
7. Bob then calculates the message digest on his side, and sees that it matches the digest he just decrypted using Alice's public key, and so with this he knows that Alice must've sent it, and it wasn't tempered with!

And that's it, now we have authentication and message integrity! So how we add the confidentiality above to that? Well, we can just glue both pieces together:

1. Alice first computes the message digest and digitally signs it, generating the package message + signed (encrypted) message digest.
2. Alice generates the random session key, and encrypts the package with it.
3. Alice then uses Bob's public key to encrypt the session key, and proceeds to the package + encrypted session key.
4. Bob then proceeds to use his private key to decrypt the session key, then uses the session key to decrypt the package.
5. Once the package is decrypted, Bob can use Alice's public key to decrypt the message digest, and compare to his own computation of it. If it matches, he knows that nobody was able to read the content, it hasn't been tempered with, and it's from Alice!

Boom! Confidentiality, message integrity, and authentication.

## Pretty Good Privacy (PGP)

PGP is one of the most widely used email encryption schemes nowadays. It was first built inside US government walls, but it eventually leaked out, and it spread out throughout the world.

PGP uses basically the last scheme presented above, with confidentiality, message integrity, and authentication. It can use many of the encryption algorithms cited, such as DES, RSA, SHA-1, and so on.
