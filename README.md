# system-design-notes

## OSI Model(Open System Interconnect Model)
* Lets say there are 5 internal IP addresses connected to Router
  * 10.0.0.1 (Router) - A
  * 10.0.0.2 (Client-Computer connected to Router by wired) - B
  * 10.0.0.3 (Server-Computer connected to Router by wired) - C
  * 10.0.0.4 (Client-Computer connected to Router by wired) - F
  * 10.0.0.5 (Client-Mobile connected to Router by wifi) - D
* Layers 
  * client
  * Application Layer 7 prepares (GET / 10.0.0.3 80 --> HTTP Headers cookies, Content-Type etc)
  * Presentation Layer 6 Encrypt if necessary(HTTPS)
  * Session Layer 5 Establish Session tag (For ex: Session Id)
  * Transport Layer 4 breaks data into each sigment, And sigment may contains (123| Add ports/Seq| 80) and lot of packets
  * Network Layer 3 takes sigment data(Contains multiple packets) and send it to network Ex: (10.0.0.5 | packets| 10.0.0.3...etc)
  * Data Link Layer 2 takes packets into frames(small chunk of packet) and Ex: (D Mac Address|frame| C Mac Address). IP Adress can be reverse engineered and can find Mac address.
  * Layer 1 Physical Layer takes frames into bits and it doesn't know where to send it. Then it send's data to every where. Network card receives and sniff it off if frame doesn't belongs to respective machine.
  * server side same layers act to get data.

## Queue vs Pub/Sub
* Queue: Message published once, consumed once
* Pub/Sub: Message published once, but consumed many times

## Redis
#### Key-Value Store
* Redis is Key-Value store NoSql database
* Key is a string, value is pretty much anything
* Redis is in memory fast
* Set key with expiry
* Single Threaded(Except when durability is enabled)
#### Optional Durability
* Journaling(append only log AOP)(What happend to the system{someone inserted key, some one deleted key, etc.. can trace})
* Snapshotting
* Both happen asynchronously in the background
#### Transport Protocal
* Uses TCP
* Reuqest/Response just like HTTP
* Message format is RESP(REdis Serialization Protocol)
#### Pub/Sub
* Redis Supports Publish Subscribe model
* Push model support
#### Replication/Clustering(Avalability)
* Replication - One Leader many followers model
* Clustering - Shard data accross multiple nodes
* Hybrid(both Replication/Clustering)
#### Operations
* Set key value
* Set key with Expiry
* get Key
* Exists key
* del key
#### Setup
* Docker spinup
* default port 6379

## ZeroMQ
#### What is ZeroMQ?
* Messaging Library(20 languages)
* 5 messaging Patterns
* Brokerless
* You build what you need
* Not Sure why it's called MQ
#### Messaging Patterns
* Sychronous Request/Response
* Asynchronous Request/Response
* Publish/Subscribe
* Push/Pull
* Exclusive Pair
#### Socket Types
* REQ(Request)
* REP(Reply)
* PUSH
* PULL
* DEALER(Client)
* ROUTER(Server)
#### Thoughts on ZeroMQ
* Pros
  * Simple
  * Great for small usecase
  * Efficient Lightweight
* Cons
  * Feels over-engineered could be simpler
  * You have to write your own apps
  * Could be big task if you need Pub/Sub

## Kafka
### Consumer Group
* To act like Queue, put all consumers in one group
* The partitions are alocated to the each individual consumer in same group
* The consumer never know about partitions which are allocated to other consumer in the same group
* To act like Pub/Sub, Put each consumer in a unique group
* then one partition can be consumed by multiple consumers
* we get parallel processing for free
