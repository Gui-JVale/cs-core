---
sidebar_position: 2
---

# Cryptography Principles

## Introduction

Cryptography dates back to old Egypt, and Julius Cesar. It has being used to protect information for centuries, specially in times of war where it's of much interest to protect crucial war information from the enemy party. Large books can (and have been) written about the history of cryptography, also about the field itself.

The goal here is not to view the subject in great detail, but to have an understandable big picture view of things, and be able to reason about it on the context of networks.

As we've seen, networks are all about communication, exchange of data in bytes. Whenever there's communication between two or more parties, there can be bad guys listening to it to try to grab important bits, such as passwords, bank account data, confidential government records, etc. And so it is of crucial importance to disguise this information in the case that it in fact gets intercepted by a bad guy. Assuming the method used to disguise or encipher the data (the cryptography algorithm) is strong enough, it's extremely unlikely that the bad guy will be able to decipher the data if intercepted.

Also, an obvious, but extremely important point is that the receiving party must be able to transform the enciphered data back to it's original form (if not the whole purpose of the communication is lost!).

There are basically two classes of encryption systems: **symmetric key cryptography**, and **public key cryptography**.

## Symmetric Key Cryptography

Symmetric Key Cryptography has been used for centuries, dating back to the famous Julius Caesar, in which it was used to encrypt war messages between parties, the **Caesar Cypher** is very simple, and greatly summarizes this type of encryption, so let's take a deeper look:

To encrypt a message parties agreed upon a **shared key**, in the case of the Caesar Cypher, this was an integer that represented an alphabet offset, so for example if the key was 3, to **encrypt** the data, the letter "a" would be transformed into the letter "d", "b" into "e", and so forth, wrapping around if the sum passed 26. Once the message was received, the receiver used the same key to do the opposite process and **decrypt** the message.

Let's say Alice wants to send a message to Bob:

`Bob I love you, Alice.`

Using the Caesar Cypher with the key = 3, this would be encrypted to:

<!-- cSpell:disable-next-line -->

`ere, l oryh brx. dolfh.`

Because of it's simplicity, the Caesar Cypher can be easily broken. Let's say and intruder Trudy hates Alice and Bob, and wants to intercept their messages. Here are some ways Trudy can use to break their encryption scheme:

- _Ciphertext-only attack_: In some cases, the intruded may only have access to the enciphered text, not knowing about any of its original content. However, it can still be deciphered by using statistical analysis, that is, in a language (like english), there are certain patterns of communication, some letters and expressions appear way more then other, and so it's still possible to break the encryption, specially with a weak encryption algorithm like the Caesar Cypher.
- _Known-plaintext attack_: On this type of attack, the intruder has some knowledge about the content of the original message, for example he knows that there must be either "Bob" and/or "Alice" in the original message, and so he can try to decode it based on that. When an intruder knows some part of the plaintext pairings, that's referred to as known-plaintext attack.
- _Chosen-plaintext attack_: In a chosen-plaintext attack, the intruder is able somehow to choose the plaintext message, and get the ciphered version, then it can map it out to gain knowledge about the encryption algorithm and key. An example is Trudy somehow makes Alice send the known message: `The quick brown fox jumps over the lazy dog`, he then intercepts the cipher and discovers the key.

This one letter always maps out to the same other letter symmetric encryption scheme is known as **monoalphabetic cipher**, and as seen above, it's very simple to decode. A more robust version of this is **polyalphabetic encryption**, in which the same letter can be encrypted to different letters, which can be done using different keys and alternating them in each letter, making it harder to decode the message. To add more robustness, some randomness can also be added on top of this in clever ways.

Symmetric key encryption is still widely used to this day in networks with block cipher algorithms. Some of the algorithms used in practice are DES, 3DES, and AES.

One very important factor that has been left unsaid so far is that **both parties must agree upon a shared key**, which presumes secure communication in the first place (what a paradox!). In the context of networks, one party would have to first send the private key over to the other before they start exchanging data (through a possible insecure channel), and so how would parties that never met, and possibly will never meet again, exchange secure data? As we'll see next, there's another clever and elegant encryption system which doesn't required the exchange of keys between parties beforehand.

## Public Key Encryption

Considering how many years encryption has been around, public key encryption is relatively new, being developed in the 70s in MIT, and made possible by researches in theoretical mathematics, more specifically number theory, and modular arithmetic.

Without going into mathematics deeply, public key encryption is very simple. Let's say Alice wants to send a message to Bob without Trudy knowing it's content. Bob creates a pair of keys, one public key K<sup>+</sup><sub>b</sub> which he shares with _everyone_, including Trudy, and a private key K<sup>-</sup><sub>b</sub>, which he keeps to himself. Alice then encrypts the message _m_, by calculating _K<sup>+</sup><sub>b</sub>(m)_, and sends to Bob. Bob then decrypts the message by calculating _K<sup>-</sup><sub>b</sub>(K<sup>+</sup><sub>b</sub>(m))_. That's public key encryption in a nutshell.

With this scheme, two worries may come to mind. First, the intruder Trudy has access to both the encryption key, and the encryption algorithm, so one may think that he can easily coordinate a chosen-plaintext attack and break down the encryption system. He may as well try, but for this system to be robust the pair of keys must be generated in a way that's extremely hard, or nearly impossible to get the private key by using the public key and the encryption algorithm. Second, and more of a real concern, because both the key, and the algorithm are made public, Trudy can pretend that he's Alice, and send an encrypted message to Bob, with symmetric key this wasn't an issue because by sending the encrypted message it was implicit that it came from the expected sender, since he had the other key.

In practice, the algorithms widely used for public key encryption is **RSA**. The drawback of RSA is that it's computations can be very consuming and slow, so in practice both public key, and symmetric key encryption are used for secure communication. This works with **session keys**.

### Session keys

If Alice wants to send a large message to Bob, one that would take a while to encrypt and decrypt with RSA, Alice can generate a session key K<sub>s</sub> that will be used for symmetric encryption (using DES) during a message exchange session between her and Bob. She then uses public key encryption (with Bob's public key, using RSA), to encrypt the session key, and send it over to Bob. Now they can both encrypt large amounts of data using less taxing symmetric key encryption.
