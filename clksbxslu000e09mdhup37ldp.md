---
title: "Event Driven Approach of NodeJS"
datePublished: Tue Aug 01 2023 13:23:18 GMT+0000 (Coordinated Universal Time)
cuid: clksbxslu000e09mdhup37ldp
slug: event-driven-approach-of-nodejs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690893813747/2352b3fd-a308-41af-b5ed-e7b5cf0329c2.gif
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690897734832/f391db22-1c7a-4892-95e0-602f1065bbf2.gif
tags: nodejs, developer, best-practices, event-driven-architecture, 90daysofdevops

---

**NodeJS** gives the facility of an **event-driven approach** in our application development. Due to this approach, we get the power **to do multiple activities concurrently** on the trigger of a particular event.

Here, let's focus on-  
1)      What is Event Driven Architecture?

2)     How NodeJS gives the ability to emit & listen to events?

1. How observer pattern gets used in NodeJS?
    

4)     How to create Custom events in NodeJS?

## 1\. What is Event Driven Architecture?

Event listeners react to **emitted events** by **calling the event handler functions.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690895324325/5206bd18-87ff-476f-a20a-447ae58eae49.png align="center")

Most of the CORE node modules **like http, fs(file system), timers etc**. all are built around event-driven architecture

## 2\. How NodeJS gives the ability to emit & listen to events?

Any object which is inherited from the **Event Emitter class** on that object we can emit and listens to the event. And this event emitting & listening logic is called an observer pattern in JavaScript.

Let’s see this in more detail below example,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690893714536/f455aac6-a7e3-4c18-9d53-f8fa6d5f0ffc.png align="center")

**Note:** Server object is inherited from EventEmitter Class. So, the server object inherits **all logic of event emitting and listening** from EventEmitter class.

## 3. How observer pattern gets used in NodeJS?

Whichever object in Node.js that is inherited from the EventEmitter class can emit events and listen for events on that object

**This event emitting and listening logic** is called **Observer Patten in JavaScript**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690894216049/f0fb76fb-7b55-491d-9009-e45babe40768.png align="center")

•Here, the event listener is continuously observing the subject (i.e. event emitter) to emit an event

•<mark>Observer pattern has been designed </mark> **<mark>to react</mark>** <mark> rather than </mark> **<mark>to call</mark>**

Opposite to this is,   **Function calling other functions**  to this we are very used to which is not much reliable here

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690894490342/398f7632-8c61-48a7-a6a4-6882bef7a5ca.png align="center")

## 4\. How to create Custom events in NodeJS?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690895005442/53d8c72e-56f7-4f43-a2ea-0578501c3198.png align="center")

In this way, on **"emit"** of such events **<mark>we can implement multiple handlers.</mark>** And we can achieve concurrency of multiple activities of our application.

![666 Emoji Copy And Paste](https://i.pinimg.com/originals/e2/0f/86/e20f8642956cfbe92c58f52a58f85242.png align="center")

## Happy Coding