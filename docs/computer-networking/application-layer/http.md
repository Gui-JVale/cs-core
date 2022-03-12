---
sidebar_position: 2
---

# HTTP

HTTP (Hipertext Transfer Protocol) is a protocol that dictates how a client and a server should communicate. It specifies rules as to how requests and responses should be made.

**It's a pull protocol** because the client asks for the data from the server on demand.

**It uses TCP** on the transport layer, thus this protocol is **connection oriented** and provides **reliable data transfer** between hosts.

A connection established using HTTP is said to be **stateless**, as the server doesn't keep any state from previous connections with any clients. This allows web serves to be very performant, and manage many TCP connections simultaneously. However, some sort of state can exists with the use of **Cookies**.

## Non-Persistent and Persistent Connections

**By default** an HTTP connection is non-persistent, that means **every time a client needs data from the server, it needs to establish a new connection**.

In practice, it works like this: the client requests a web document (a html file), then every single time the client finds an object in that file (an image, css/js files etc), it needs to establish a new connection with the server to get that object. Now this can be very wasteful, and slow.

**By using special a header field, a client can ask for a persistent connection with the server**. This allows the client to get all the objects it needs for that initial html document from a single connection. The server can then terminate the connection after not hearing from the client for a period of time.

## HTTP Message Format

A HTTP Message consists of a **request or response line** followed by a carriage return and a line feed, then a set of **header fields**, followed by a blank line consisting of a carriage return and a line feed (to separate the header from the body), and finally the **message's body** containing the actual data.

If it's an HTTP Request, the request line consist of an **HTTP Verb** (GET, POST, PUT, DELETE...), a space, a url, another space and the HTTP protocol version, this line is terminated by a carriage return and a line feed. In practice it looks something like this:

```
GET /example/url HTTP/1.1
```

If it's an HTTP Response, the response line consist of the HTTP protocol version, a space, an **HTTP Status Code** (200, 301, 404, 500...), and optionally a space and a status message ("OK"). This line is terminated by a carriage return and a line feed. In practice it looks something like this:

```
HTTP/1.1 200 OK
```

Each header field is a one liner consisting of a key, a colon, an optional space and the value followed by a carriage return, and a line feed. It looks something like this: `Content-type: json`.

Here's an example of a HTTP request:

```
GET /example/url HTTP/1.1
Content-type: json
Keep-Alive: 100
Host: www.google.com
```

and a response:

```
HTTP/1.1 200 OK
Keep-Alive: 100
Host: www.google.com

{ "data": "this is the actual data" }
```

## User Cookies

As stated before, an HTTP Connection is stateless, but what if a company wants to personalize their customers experiences a bit? **Is there a way to keep state of each client?** As you probably guessed, the answer is **yes, and the mechanism, Cookies**.

Cookies are a simple way to keep state between client and server, and it starts with the server response message, asking the client to set some cookies on it's host, using the header field Set-Cookie. The client browser then stores the server cookies in a file on the users machine, that's managed by that browser.

Now **every time the client requests something from that server, it also sends this cookie**, which the server uses to query the user state in a database, and provide a more personalized experience.

## Web Caching

Caching is a big part of the internet (and it's performance), and it happens in many levels. Web caching allows for data to be fetched faster, providing a better experience for the user. This allows for a company to serve content fast event though the user may be far from it's data center.

**A company can use proxy servers or a Content Delivery Network (CDN) to have server closer to end users**, and cache web content in those servers, avoiding the round-trip time (RTT), and the time it takes to send the data. This way, when a client requests a web page, the server first tries to serve it from the cache, and if it's not there, it fetches from the data center server and then caches it.

**What about web servers that serve dynamic content?** It can still be cached. The only difference is that, if there's a cache hit, before the cache server sends the response back to client, it sends a **conditional GET** request to the web server on the data center, using a header field "Last-Modified", if this field's value, sent by the cache serve, matches the value from the data center web server value, the cache server then just responds to the client with the cached document. Otherwise, because of the conditional GET, the cache server downloads the new document from the server, sends to the client and updates it's own cache.
