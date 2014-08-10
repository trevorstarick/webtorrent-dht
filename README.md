webtorrent-dht
==============
A Distributed Hash Table framework for NodeJS and Javascript ES5/6

![node.js is shiny](http://feross.net/x/node2.gif)

## Project Goal
Using [WebSockets](http://socket.io/)/[WebRTC](http://www.webrtc.org/) and [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)/[LevelDB](https://code.google.com/p/leveldb/) to create a mesh network of clients without the need of servers. 

## Database Structure
```
┌── chunk0
│	└──	client0 (initial client)
├── chunk1
│	├── client0
│	└── client2
├── chunk2
│	├── client0
│	└── client1
├── chunk3
│	├── client0
│	├── client1
│	└── client3
├── chunk4
│	└── client0
└── chunk5
	├── client0
	└── client3
```

### Requesting Data
Lookup for chunkX and it returns a list of clients who have broadcasted they have finished downloading said chunk. You would then request from one or more of the clients "Can I have chunkX" and wait for the first response. The first response would generaly be the fastest connection due to location geographically or bandwith/speed. Once you finish fetching chunkX from clientY you would callback with a broadcast declaring that you have gotten chunkX and are ready to upload.

## Links
- [Kademlia](https://en.wikipedia.org/wiki/Kademlia)

