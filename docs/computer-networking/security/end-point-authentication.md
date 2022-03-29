---
sidebar_position: 4
---

# End-Point Authentication

## Introduction

As we've briefly discussed, authentication is the act of verifying someones identity, making sure they are who they claim to be. As humans we authenticate all the time without even noticing it. Looking at someone's face, recognizing their voice over the phone, the officials who check for your ID or Drivers License picture and compare it to your face, those are all forms of authentication. If you pay close attention, you'll notice that all this forms of authentication are biometric based, they rely on biological aspects one way or another. The challenge of authentication on computer networks is that we can't really use biometric authentication, so we must come up with other ways to prove that a computer is who it's claiming to be, for example proving that a router is a router and not an intruder, proving that the Amazon server you're sending your credit card information to it's actually an Amazon server, and not a hacker trying to steal your payment info, and so forth.

This is where end-point authentication comes in, it aims to authenticate both parties of a communication over the network, so that they can safely proceed to exchange data without having to worry with security reliabilities. Observe that this must happen "on the fly", without any beforehand knowledge about who a host is going to communicate with, for example servers don't actually know anything about a client before they try to establish a connection.

And so with this challenges in mind, and our new knowledge of encryption, let's iteratively try to come up with end-point authentication.

## Designing End-Point Authentication

Let's again say that Bob and Alice want to communicate over a network, and an intruder Trudy, is trying to do bad things with their communication and data.

Well, the simplest way would be every time Alice sends a message to Bob, she can say: "I'm Alice". By now you should know how bad this is, Trudy can just send a message to Bob with "I'm Alice", and easily break their authentication scheme.

Let's try again, instead of saying "I'm Alice", Bob can know Alice's IP address, and then check if the datagrams are coming from there, this way he knows it must've come from here, and nobody else. Wrong! By now you should also know that it's not that hard to forge IP datagrams, and so Trudy could simply put Alice's IP address as the datagram source, and send it to Bob. Another flawed authentication.

Ok then, so what about a password? Yea that sounds nice, passwords are used everywhere, they are safe right? So Alice, and Bob agree upon a password, a symmetric key, and then send that password along with each message, proving to each other who they are. Well, the obvious flaw here is that Trudy could eavesdrop the communication, learn about the password and then forge messages at will. So naturally, we can use our new cryptography knowledge, and encrypt the password and the message before sending it over, this adds confidentiality, and message integrity depending how it's done. However, there's still a subtle,but very important flaw in this method. Trudy can eavesdrop a message going from Alice to Bob, and then re-send the message later on, Bob receiving the encrypted message with the correct password, would never suspect that it didn't come from Alice. Another flawed authentication.

Alright, we're getting there, so how do we solve that important flaw on the last authentication method? Well, that's a problem that TCP had, and already solved! The problem being, how could a server know if the segment is coming from the actual client, or it's just being played back by a bad guy? The solution is introducing a **nonce**, a random generated number that's used once during the communication. To use it, Alice sends her first encrypted message to Bob with their shared secret, Bob then replies with a random number _R_, Alice then encrypts the nonce with their shared secret, and sends it back to Bob, Bob decrypts the message, and see it matches _R_, they are now authenticated.
