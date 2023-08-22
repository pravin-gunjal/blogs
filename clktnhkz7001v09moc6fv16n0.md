---
title: "Streaming using NodeJS"
datePublished: Wed Aug 02 2023 11:34:23 GMT+0000 (Coordinated Universal Time)
cuid: clktnhkz7001v09moc6fv16n0
slug: streaming-using-nodejs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690975926080/c0fded88-6974-42e7-aeee-ee710312cb50.gif
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690976037877/0709b56e-ae12-4699-8bc7-3ea212a163d5.gif
tags: nodejs, devops, node, nodejs-developer, 90daysofdevops

---

Here, We learn about-  
1\. What is Stream?  
2\. How many types of Streams?  
3\. What is it's(stream) advantage?  
4\. How to create it using NodeJS?

## What is Stream?

When we try to read data from any large file on the server or try to write data in a particular file then Node JS tries to store that data in the buffer <mark> all at once.</mark> This is shown below example,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690970721738/78574704-564c-4df8-abae-8e6eba92a0fd.png align="center")

If we make use of a stream, then we can read/store data <mark>in the form of small chunks</mark> as data get received in the stream buffer like below:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690971420035/08629806-1d77-4313-ab87-1e4892f68db0.png align="center")

## How many types of Streams?

There are <mark>4 types of streams</mark>. But readable and writable are gets used mostly. These are listed below:  
**1\. Readable Stream:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690971967132/e36086a5-14b1-4ed2-bbb5-3187aa2886e0.png align="center")

**2\. Writable Stream:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690972106913/01a40f30-6620-4f69-b17d-719ebe9169d8.png align="center")

**3\. Duplex Stream:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690972324579/be834407-ef3b-4c81-9d3c-b3495922e23a.png align="center")

**4\. Transform Stream:**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690972568813/2032517d-c162-49d9-90cc-253613a62b3a.png align="center")

## What is the advantage of Streams?

The main advantages of streams are as follows:

* **Memory Efficiency:** Streams process <mark>data in small chunks,</mark> reducing memory consumption for large datasets.
    
* **Performance:** Streams <mark>enable asynchronous processing, </mark> improving overall performance and <mark>response times.</mark>
    
* **Backpressure**: Streams support the backpressure mechanism, making use of the <mark>pipe method </mark> (Note: This is one important concept which I have explained in one of the below examples where I have explained how to create a stream). In short, this ensures data flow(coming in stream & reading/writing from stream).
    

## How to create a stream using NodeJS?

Lets us understand this with one example:

```javascript
server.on('request', (req, res) => {
    let rs = fs.createReadStream('./Files/large-file.txt');
    rs.on('data', (chunk) => {
        res.write(chunk);
    });
    rs.on('end', () => {
        res.end();
    })
    rs.on('error', (err) => {
        res.end(err.message);
    });
});
```

In the above example, <mark> I have created a readable stream</mark> which reads data in the <mark>form of data chunks</mark> from one very large file(having millions of data lines).  
Here, I have taken a text file. We can make use of different file formats like video, audio, JSON etc.  
**Let's dive into some details of this example:**  
In this example,  
**Step 1**. I have created one read stream i.e **rs**  
**Step 2.** On every chunk of data coming into this buffer **'data'** event gets emitted and each time that chunk gets written into the res object  
**Step 3.** After completing the whole data read from the file **'end'** event gets emitted and the next operation takes place.  
Note: This example is an alternative to the example of which I have taken at the very first of this article

In this way, streams help in our application for large file reads/writes and <mark>ultimately speed up our application</mark>.

Hope this article helps you in your coding journey. If yes then like and share this article on your social media/tech platforms so that this will help our community.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690975737682/d2d4cd42-dbe7-4b5c-bed3-b3c9e6fd11d2.jpeg align="center")

\~~~~~~~~~~~~~~~~ Happy Coding ~~~~~~~~~~~~~~~~~~