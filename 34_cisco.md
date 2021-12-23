name: main

### .aim[Systems: Cisco in an Hour™ IV: A New Hope]
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

.center[![star wars](assets/l34_starwars.png)]

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

???
$ cat /etc/services
list of ports

---
template: main

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

#### Application Layer

Once a socket (transport layer connection) has been established, the data transmitted between computers is at the application layer.

Think about the data/payload section of an IP packet, anything inside that is application layer inforation.

Data at this layer will be packaged depending on the program or protcol being used.

Common application layer protocols: http, ftp, ssh, dns...

Many application layer applications have registered ports at the transport layer.

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


---
template: main

Cisco in an Hour

Cisco in an Hour 2: Electric Boogaloo

Cisco in an Hour 3: In 3-D

Cisco in an Hour IV: A New Hope

Cisco in an Hour V: for Vendetta

Cisco in an Hour VI: The Undiscovered Country
