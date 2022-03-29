---
sidebar_position: 3
---

# Message Integrity and Digital Signatures

## Introduction

We've seen in the last chapter how we can achieve confidentiality in networks (and in communication in general), by using encryption algorithms. While this is a big step towards a secure network, we're still not there quite yet, there are still some properties missing such as **message integrity**, and **authentication**.

To speak in more practical terms, say Alice wants to send a private message to Bob, by using the techniques we covered, she's able to robustly encrypt the message and send it to Bob. However, the intruder Trudy is a smart ass, and knows that it's nearly impossible for him to decrypt the message once intercepted, so instead he just tempers with the data, altering it's contents before it gets to Bob. Once Bob receives the data, he might not be even able to decrypt it anymore, not cool Trudy!

And we also haven't covered the case where Trudy pretends to be Alice, and sends a message to Bob.

So by looking at this simple cases, we can't tell that we don't yet have secure communication with just confidentiality, but we're getting there.

Let's take a look at message integrity first.

## Message Integrity

The goal of message integrity is pretty simple, ensure that the receiver is able to verify if the message hasn't been tempered with and that the sender is legitimate (not forged), in other words, **confirm that the message's integrity has been kept**.

To achieve message integrity cryptography comes to rescue once again, this time in the form of **cryptographic hash functions**.

A cryptographic hash function is a function that takes in an input _m_ and computes a fixed-size string _H(m)_ known as **hash**. This functions have the additional property that it is computationally infeasible to find any two different message x and y such that _H(x) = H(y)_. This means that it should be infeasible for an intruder to replace a message x with y and still get the same hash.

So then to send a message _m_, the sender computes the hash _H(m)_ using a cryptographic hash function, and sends the pair _(m, H(m))_. Once the receiver gets the message, it computes _H(m)_ (with the same hash function), if both hashes match, then the message hasn't been tempered with. Observe that this does not provide confidentiality, if that's also needed, then both parties must symmetric and/or public key encryption on top of the hash functions, this works well for routers computing distributed routing algorithms, who are only concerned with integrity, and not confidentiality.

Most widely used hash functions today are **MD5**, and **Secure Hash Algorithm (SHA-1)**, the latter being a government standard.

### Message Authentication Code (MAC)

Ok so let's put to practice what we just learned, using Alice, Bob, and Trudy!

1. Alice wants to send a message _m_ to Bob, so she computes the hash of the of the message _H(m)_ using SHA-1
2. Alice then appends the hash to the message, creating _(m, H(m))_, and sends it to Bob .
3. Bob receives her message, and calculates the hash _H(m)_, it checks that the hash matches the one received, and so the message has kept its integrity.

There's an obvious flaw here, and that is that Trudy can still pretend he's Alice and send a message _(m', H(m'))_. Bob would inspect the message, and everything would checkout, so he wouldn't suspect anything.

To prevent this, and achieve message integrity, Bob and Alice need a shared secret _s_, this share secret, which is nothing but a string of bits, it's called **authentication key**. Using this shared secret, message integrity can be achieved as follows:

1. Alice creates message _m_, then, concatenates _s_ with _m_, creating _m + s_, and then computes _H(m + s)_. _H(m + s)_ is called the **message authentication code**.
2. Alice then sends _(m, H(m + s))_ to Bob.
3. Bob, who has _s_, upon receiving the message _(m, h)_ he calculates H(m + s), and sees that _H(m + s) = h_, and so he knows it was in fact sent by her.

The most popular standard for MAC today is **HMAC**, which can be used either with MD5 or SHA-1.

As you may be imaging, there's still the important issue of distributing the authentication key, as we've seen, this can be done confidentially using public key encryption.

## Digital signatures

How many times have you been required to sign something? Either a document, a check, or a receipt. Have you ever stopped to think about the meaning of it? Your signature attests that you (as opposed to somebody else), have acknowledged, or agreed upon the contents of the document.

What about signing something digitally? Is that even possible? For it to be possible, it must be **verifiable**, that is another person or entity can in fact verify that the document was signed by another person, and it must also be **nonforgeable**, meaning it can't be faked. Well, we'll see that with the help of some of the cryptography things we went over that is, in fact, possible.

Remember public key encryption, and it's elegant way to encrypt data without the need to first agree upon a symmetric key? The elegancy of that method carries over to digital signatures, in a slightly different, but very similar way.

So let's say Alice is in court, and she wants to prove that Bob digitally signed a document _m_, and further that the _m_ hasn't been tempered with. Let's start on how Bob would sign the document in the first place. He generates the usual pair of private key _K<sup>-</sup>_ and public key _K<sup>+</sup>_, then using his **private key** he computes _K<sup>-</sup>(m)_, and that's his signature! Now one may think how would this be a digital signature? Well, let's go back to Alice proving that Bob signed in court: Alice takes in Bob's signature _K<sup>-</sup>(m)_, and then uses his **public key** (that it's known to be Bob's) to compute _K<sup>+</sup>(K<sup>-</sup>(m)_)\_ and voila! The document is back to it's exact same format, not only proving that Bob signed it using his private key, but also that it hasn't been tempered with, providing integrity as well.

As you can see, this makes the signature verifiable, because when computing with the public key the original document appears exactly the same, so only Bob's private key could've signed it. It makes it also nonforgeable, because if someone else tries to sign it, and claim it was Bob, Bob's public key won't be able to bring back the document to how it was, so it must be that Bob didn't sign it! Boom, digital signatures!

Many digital signatures work like this, with the slight difference being that usually the signature is not computed on the entire document, because these can be computationally expensive, so instead a hash of the document (which as you rememeber is a fixed-length string that represents the document) is used to compute the digital signature. In practice, it works like this:

1. There a document _m_ which Bob wants to sign with his pair of keys _K<sup>-</sup>_ and _K<sup>+</sup>_
2. Bob uses a hash function (like SHA-1) to compute _H(m)_
3. Bob uses his **private key** to compute _K<sup>-</sup>(H(m))_, and that's his signature.
4. Alice wants to verify that Bob in fact signed _m_
5. She proceeds to compute the hash of the document (using the same hash function as Bob) _H(m)_.
6. Alice gets Bob's signature _s_, and with Bob's **public key**, she computes _K<sup>+</sup>(s)_
7. Alice verifies that _K<sup>+</sup>(s)_ = _H(m)_ and so Bob must have signed it.

### Public Key Certificates

An important problem that arises from the digital signature method explained above, is the verification that a certain public key in fact belongs to the person who signed the document. Think of this scenario: Alice is expecting a message from Bob, she receives a message from Trudy, claiming he's Bob, and signs the document with his private key, and sends over his public key along with the message, Alice verifies that the signature is legitimate, so she thinks she's talking with Bob.

To solve this issue, we need a certificate issued by a **Certification Authority (CA)**. A CA's job is to verifies that the person, router, server, etc. is who it claims to be, and then it generates a **certificate** that binds the identity with a public key. The certificate is digitally signed by the CA.

With this, Bob along with his signature, also sends to Alice his certificate. Alice then, using the CA's public key verifies that the certificate is legitimate, and then proceeds to extract Bob's public key, and check Bob's signature.
