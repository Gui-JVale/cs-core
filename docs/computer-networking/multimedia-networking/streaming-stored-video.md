---
sidebar_position: 2
---

# Streaming Stored Video

## Overview

On stored video streaming, the videos sit on the server, and the users requests the content on demand.

Streaming stored videos has it's own set of properties. First, the user will be downloading the video while consuming it (that's the streaming bit). Second, there must be interactivity, such as the user being able to pause, fast-forward, or go back, with acceptable responsiveness. Third, the user expects continuous in order playback of the content, not tolerating many freezes, or corrupted data.

Streaming stored video can be divided in three categories: **UDP streaming**, **HTTP streaming**, or **adaptive HTTP streaming**. In practice, all three are used by different applications, but the most systems today employ adaptive HTTP streaming.

A characteristic that all categories share is the extensive use of **client-side buffering** on the application layer. That is the client application keeps a buffer with the incoming data, this buffer refers to the part of the content that is downloaded from the server but not seen yet by the user. Consequently, if the user consumes data from the buffer faster than it gets there, the experience won't be ideal. The buffer allows some room for delays.

## UDP Streaming

UDP streaming relies on the fact that UDP doesn't have flow, or congestion control, so packets can flow continuously from server to client. Reliability must be implemented on the application layer here.

While this may seem like the way to go, it has three significant drawbacks. First, the unpredictable, and varying bandwidth available between client-server can fail to provide continuos playback for the client, leading to poor experience. Second, there must be a separate server to handle the interactivity of pause, fast-forward, etc. Which adds a lot of complexity, and overhead. Third, many firewalls block UDP traffic, and so UDP streaming wouldn't work for users sitting behind this kind of firewall.

Because of this, applications tend to refrain from UDP streaming.

## HTTP Streaming

On HTTP streaming, the video file is stored in a normal HTTP server addressed by an url. To see the video, the client can issue a GET request to the server url, establish a TCP connection, and then download the content.

A drawback of this method is that once the user issues the request for a video, it will only download that version of the video. As discussed previously, videos can be compressed into multiple versions, and so what can happen is the user requests a high-quality version of the video, because in the moment of the request it has high bandwidth, then for some reason, in the middle of the connection, the client's bandwidth decreases significantly, or the network gets congested, this would lead to a poor experience with frozen screen, and lots of waiting time.

In early days, it was thought that streaming applications would never be able to run using TCP, due to it's 'saw-tooth' behavior, and the variable rate at which data gets transferred, due to it's flow, and congestion control mechanisms. However, it was learned that streaming can be done using TCP. One of the factors that contribute to that was using pre-fetching of the video, keeping some bytes on the client-side buffering, allowing some room to breathe for the TCP's varying data rates.

On HTTP streaming, there's no need for a separate server to handle interactivity, this can be handle simply with a GET request, the client can request the bytes of the video that it wants to see on demand.

A good thing to note here is the relationship between the client-side buffer, and the TCP buffer. The TCP buffer feeds the application buffer, which is consumed by the user, and so if both buffers are full, data will go from the TCP to the application buffer at the pace the user watches the video.

Another thing to point out is early termination and repositioning. Because of the nature of the buffers, every time a user repositions, or terminates the video early, all the data in the buffers that weren't consumed yet get thrown away. This can lead to a lot of waste of valuable resources on the Internet.

Due to the factors stated above, HTTP streaming has enjoy wide deployment in applications.

## Adaptive HTTP Streaming with DASH

As stated above, one drawback of plain HTTP streaming is the fact that users download only one compressed version, which is not a very resilient way to deal with the networks varying bandwidth, and unpredictability. So how do you deal with a problem like this? Enters adaptive HTTP streaming with DASH.

Wouldn't be better if the client could, instead of choosing one version and sticking to it, download chunks of the video on demand based on it's current available bandwidth? This adds a lot more resilience to the process, let's take a look at an example: when the client starts downloading the video, it has a lot of bandwidth, and the network is not very busy, so it chooses a high quality version of the content, and starts downloading. The catch here is that the client doesn't download the entire video, but only the first chunk with the quality it chooses. Once that chunk hits a consumption threshold, the application, based on measurements of the connection with the server, can request another chunk of the video, and base it's compression decision on the measurements it made. So let's say the network performance took a hit, then the application request a lower quality version of the video, and so.

That's the advantage of DASH, it **adds more resilience to streaming**. In practice, the serve keeps a **manifest file** with the versions of the video, and it's respective urls, the client then first request this manifesto file, and starts requesting chunks based on it's current available bandwidth, and network measurements.
