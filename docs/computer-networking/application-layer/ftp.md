---
sidebar_position: 3
---

# FTP

File Transfer Protocol (FTP) is used **when a user wants to transfer files to, or from a remote host**. First, the user must **authenticate** itself with a user identification and password, then user gains access to the remote file system, and can transfer file from the local file system to the remote file system, and vice-versa.

FTP, just as HTTP, **uses TCP under the hood** to have reliable data transfer. Also it uses the client server modal, where the client is the one sending the FTP commands, and controlling the remote file system, while the server sends replies.

Different then HTTP, FTP servers must maintain **state** from current users, so it knows where the user currently is in the file system, as well as user identification and password. Also another aspect that FTP differs from HTTP, is that **it must maintain two connections between client server**, one is a control connection, used to authenticate, and send information about the remote file system, and the other is used to transfer files.

## FTP Commands

- `USER username:` used to send username information to server.
- `PASS password:` used to send password information to server.
- `LIST:` used to request information about the remote file system.
- `RETR filename:` used to retrieve a file from the server.
- `STOR filename:` used to store a file in the remote file system.
