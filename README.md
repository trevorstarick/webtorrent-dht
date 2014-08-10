webtorrent-dht
==============
A Distributed Hash Table framework for NodeJS and Javascript ES5/6

**ALPHA ALERT***: Knowing me, I'll end up migrating this project into something else or be constantly changing design desicions. Please don't use this in a production enviroment unless you absolutly need to*

## Project Goal
Using [WebSockets](http://socket.io/)/[WebRTC](http://www.webrtc.org/) and [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)/[LevelDB](https://code.google.com/p/leveldb/) to create a mesh network of clients without the need of servers. Initialy this won't have support for existing Bittorrent clients but the project is aimed for large file CDNs or Video/Audio streaming services.

## Custom ChunkSize
Min of 32kB and Max of 16MB. Must be a byte size to the power of 2. Initial seed/client list will send chunksize, number of files, and size of each file. This will allow the client to partition space for each file and know how chunk distribution and partitioning should be done and preallocate said space for the lookup.

## Database Structure
```
client0 is the initial seeder
client 1-3 are new peers

┌── chunk0
│	└──	client0
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
**Note:** Each chunk is SHA-1 hashed to prove that it is still valid once downloaded. Chunk values will be an array of hashed client ID's or something like that.

### Requesting Data
Lookup for chunkX and it returns a list of clients who have announced they have finished downloading said chunk. You would then request from one or more of the clients "Can I have chunkX" and wait for the first response. The first response would generaly be the fastest connection due to location geographically or bandwith/speed. Once you finish fetching chunkX from clientY you would callback with a broadcast declaring that you have gotten chunkX, it is valid and are ready to upload.

## Links
- [Kademlia](https://en.wikipedia.org/wiki/Kademlia)
- [DHT](http://en.wikipedia.org/wiki/Distributed_hash_table)
- [Mainline DHT](http://en.wikipedia.org/wiki/Mainline_DHT)
- [BitTorrent DHT Standard](http://www.bittorrent.org/beps/bep_0005.html)

![node.js is shiny](http://feross.net/x/node2.gif)
