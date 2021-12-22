name: main

### .aim[Systems: Cisco in an Hour™ 3: In 3-D]
<style>
.aim {
font-size: .75em;
border-bottom: 1px solid lightgray;
margin: 1px;
}
.remark-inline-code {
  background-color: lightgray;
  border-radius: 3px;
  padding-left: 2px;
  padding-right: 2px;
}
h4 {
font-size: 1.5em;
margin: 1px;
}

center_img {
  display: block;
  text-align: center;
}

.table {
  border: solid 1px black;
}

</style>

---
template: main

.center[![3d](assets/l33_3d.png)]


---
template: main

__Routing__

Routers break IPv4 packets (more later) into fragments.

When a router receives a packet, it has 2 options:

  1. Send that packet to the attached local network.
  2. Forward that packet to a different router.

Routers have address tables that identify all connected networks/devices.

---
template: main

__IP Packets__

IPv4 Packet format:

`header` `source` `destination` `data`

<hr>

--

`header` 12B: Packet metadata

`source` and `destination` 4B each: IP Address

`data`: MTU is 65,535 Bytes

???
IPv6 uses 8 Byte addresses
IPv6 allows for jumbograms, with an MTU of 4GB

---
template: main

__IPv4 packet header__

`type` `size` `fragment info` `ttl` `protocol` `header checksum`

 <hr>

--

`type` 2B: IPv4 / v6, length of header

`size` 2B: Total size of the packet

`fragment info` 4B: full payloads may be broken into multiple fragments. Each packet will count the number of fragments and its individual fragment number.

`ttl` (time-to-live) 1B: Maximum number of hops a packet can make before reaching its destination.

`protocol` 1B: TCP / UDP (this is transport layer information)

`header checksum` 2B: only a checksum of the header, not the full packet.

---
template: main

__IP Addressess__

Every device connected to the internet has an I.P. (Internet Protocol) address.

They might look like this: `149.89.150.100`  (IPv4)

or this: `0:0:0:0:0:ffff:9559:9664` (IPv6)

IP addresses are only needed when connected.

For the most part, organizations own blocks of IP addresses, and give them to their users as needed.

Because IP addresses are released in blocks, internet traffic can be routed in an efficient manner.

---
template: main

__IPv4 / IPv6 differences__

Address space: 2^32 / 2^128

Packet format: In addition to address size change, IPv6 packet headers have less information. They do not include a checksum or fragment information.

MTU:  IPv6 can allot for an MTU of 2^32 (these are called jumbograms)

IPv6 puts more work onto Link layer devices and individual hosts (computers)

IPv6 does not fragment packets at all, relying on other devices to potentially take advantage of jumbograms

IPv6 has no checksum, assuming Link layer devices and hosts will check for data integrity if needed.

---
template: main

#### Transport Layer

Computer to computer connection over a network.

Unconcerned with the individual hops of internet layer traffic.

In a program, a _socket_ is the data type associated with a transport layer connection.

Network ports are used at the transport layer that allow a computer to have multiple open network connections at the same time.

TCP and UDP are transport layer protocols.

---
template: main

#### Netowrk Ports

A network port is a computer specific sub-address that allows computers (that have a single IP address) to have multiple open netowkr connections.

There are [65,536 ports](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers).

Ports < 1024 are well known, reserved ports used for specific services.

* For example, an ssh server will have an open socket on port 22 (this is similar to a WKP). When a child process is created to communicate with a client, that process uses a different port, leaving 22 open for the listening server.

Regulated by the Internet Assigned Numbers Authority (IANA)

---
template: main

#### Transport Layer Protocols

__Transmission Control Protocol (TCP)__

* Reliable connection, guarantees delivery of data.

* Data is considered a continuous stream that arrives in the order it is sent (which may not be true in the lower layers)

* Connections are established using a 3-way handshake

__User Datagram Protocol (UDP)__

* Does not require an explicit connection, no gaurantee of data delivery (at the transport layer).

* Data is sent as discrete datagrams with a set size (as opposed to a continuous stream).

* Datagrams may be dropped, or received out of order.

* UDP connections are faster because they do not need to be reassembled at the other end.

* Error checking can still be handled at an upper level.

---
template: main

#### Data Encapsulation

As data crosses from an upper layer to a lower one, layer-specific metadata is added to help aid transmission.

Application —> Transport
* UDP or TCP headers are added, including network port information

Transport —> Internet
* Data (including Transport headers) is packaged into IP Packets.

Internet —> Link
* Packets (including IP and Transport headers) are packaged into Ethernet Frames.

???
Data decapsulation
When data crosses back up a layer, the packaging for the lower layer is removed.
