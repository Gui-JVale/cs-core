---
sidebar_position: 1
---

# Overview

## Introduction

Multimedia applications are network applications who use audio and/or video.

On the modern Internet, there's massively more multimedia traffic than just plain text documents. We're in the golden age of streaming services, every company has one. Youtube is receiving more traffic then ever, and other applications such as Whatsapp, Zoom, and Google Meets, provide real-time conversation services. Facebook, Instagram, and TikTok have videos everywhere these days (with reels).

So how does a network supports multimedia? Does it have to make some changes? Or just treat it as plain data, and call it a day?

As we'll see, video heavier than normal data, while audio has it's own set of challenges, resulting in multimedia having tighter requirements. For example, you wouldn't want to sign up for a streaming app if the video gets stuck every 5 seconds, and who would want to use the internet to make a call if the person can barely understand what the other one is saying? The nature of multimedia raises up some different challenges that we'll take a look at in this section.

## Properties of Video

The most salient property of video is it's **high bit rate**, meaning it's way heavier then audio or other types of data. To gain more insight on the proportions of how much heavier it is, let's look a simple example. Person A is scrolling through social media viewing only images and text content (no video/audio), person B is listening to Spotify, and person C is streaming Netflix. During a period of 1 hour, person C will have downloaded approximately more then 10 times data, then the other two. This means that video requires high bandwidth.

Another important property of video is that it can be compressed, at the cost of quality, and it can be compressed into multiple versions. This allows the user to choose higher video quality if his throughput permits, or stream at a lower quality if needed.

## Properties of Audio

Audio is not as nearly as heavy as video, however it has it's on set of challenges. The main one being that **we're are way more sensitive to corruption of audio**, then video. Take for example a video-conference, if the participants videos are lagging out, or freezing, the conference may continue, however if the audio is not understandable, it will come to an end.

This leads to tighter requirements, applications that rely on audio cannot tolerate much loss, and the delay has to be considerably low.

As with video, audio can also be compressed at the cost of quality.

## Types of Multimedia Network Applications

Multimedia applications can be categorized into streaming of stored video, live video/audio conversations, and streaming of live video.

### Streaming of Stored Video/Audio

Applications who stream stored video keep their content in servers (likely in CDNs), and the user is able to download the content on demand.

This category has it's own set of important properties:

- _Streaming_: The user will be watching the video while it's still getting download from the server. This allows for much less waiting time to start consuming the content.

- _Interactivity_: The user may pause, fast-forward, or back through the video. The responsiveness of this must be acceptable from a user perspective.

- _Continues Playback_: The user expects to be able to continuously consume the content without experiencing lots of delays, or a frozen screen. This leads to throughput, and bandwidth requirements.

By far the most important performance measure for video streaming is average throughput. If the hosts average throughput is less than the video bit rate, he won't be able to consume the content in an acceptable manner.

### Conversational Voice- and Video-Over-IP (VoIP)

Another set of multimedia applications are those who use real time audio and/or video. Examples are Whatsapp, Zoom, Google Meets, and so on.

Even though audio has a much lower bit rate then videos, we're must more sensitive to it, and so delay, and loss requirements are much tighter then other types of data. Because of this properties, this categories of applications are **delay-sensitive**, and **loss-tolerant**.

### Streaming of Live Video/Audio

Becoming increasingly popular, this set of applications offer real time streaming of videos/audio.

It carries many similarities to stored video streaming. The main difference being the broadcast nature of the content, which can be done in practice using IP multicast techniques, another way of doing is using P2P architecture for hosts to get content from each other.

Delay between the live action, and the stream are more tolerable than VoIP here.
