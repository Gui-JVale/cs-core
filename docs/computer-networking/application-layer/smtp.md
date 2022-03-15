---
sidebar_position: 3
---

# SMTP

## Overview

This is the protocol used to send and receive emails. It's one of the oldest protocols around, and because of that it has it's limitations, it can't encode multimedia (images, videos, audio) properly. This has made some modern email providers (like gmail), actually rely on HTTP for sending/receiving emails.

Different then HTTP, SMTP is a **push protocol**, because it pushes the data to the receiver email server. Once the receiver is ready to read it's emails, it can then download them from his email server.

As HTTP, and FTP, SMTP also **uses TCP** for reliable data transfers.

## General SMTP Scenario

Here's a common SMTP scenario for sending an email:

1. _The sender_ invokes it's user agent, using his email address and password.
2. _The sender_ writes the email, putting the receivers data, and passes it to it's user agent, to send it to his own mail server
3. _The sender's mail server_ receives the messages and puts it in a queue.
4. _The sender's mail server_ finds out the destination mail server address, and sends the email (using TCP).
5. _The receiver's mail server_ receives the email, and places it into the receiver mailbox.
6. _The receiver_ uses it's user agent to download and read the email.

Here's an example transcript of SMTP protocol once a connection is established between mail servers:

```
S: 220 hamburger.edu
C: HELO crepes.fr
S: 250 Hello crepes.fr, pleased to meet you
C: MAIL FROM: <alice@crepes.fr>
S: 250 alice@crepes.fr ... sender ok
C: RCPT TO: <bob@hamburger.edu>
S: 250 bob@hamburger.edu ... recipient ok
C: DATA
S: 354 Enter mail, end with "." on a line by itself
C: Do you like ketchup?
C: How about pickles?
C: .
S: 250 Message accepted for delivery
C: QUIT
S: 221 hamburger.edu closing connection
```

## Mail Access Protocols

Mail access protocols specify how users retrieve their emails from their mail server. They provide authentication so that other users can't just steal your mail, or take a peek.

### POP3

This is a very old, and simple protocol that allows a user agent to download emails from it's mail server. It has three phases: **authorization, transaction, and update**. Because of it's simplicity (given how old it is), it has its limitations.

On authorization phase, the user gives it's **username, and password** to get access to his emails. Then, he's able to download, and delete emails from the mail server.

On transaction phase, the users goes through it's emails, downloading them, and marking emails for deletion. There are basically two modes a client can run POP3 on, **download-and-delete, and download-and-keep**. On the delete one, when the user downloads an email, it's marked for deletion automatically on the mail server, you can imagine that this can cause trouble if the user access it's email from different devices. On the keep mode, user just downloads it, and has to manually mark emails for deletion.

On update phase, the client terminates the connection with the mail server, and th server proceeds to delete the emails marked for deletion. This implies that some sort of state must be kept by the mail server.

Another limitation of this protocol, is that the user can't organize his emails into folders across multiple devices, he can only organize it into his on local machine, the changes won't be reflected on the mail server.

The simplicity of POP3 makes it easier to implement it.

### IMAP

To overcome the limitations of POP3, and add many other features, IMAP was born. As you can guess, while POP3 it's simple, and easier to implement, IMAP is way more complex.

IMAP allows for the mail server to keep a **remote folder structure of the users emails,** allowing for the client to edit this folder structure, and see the change echo across multiple devices

### Web-based email

Due to the limitations of the old SMPT protocol, some companies have turned providing **HTTP-based mail services**. Because of the encoding of HTTP, it allows for more rich, multimedia content.
