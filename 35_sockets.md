name: main

### .aim[Systems: Socket To Me]
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

Cisco in an Hour

Cisco in an Hour 2: Electric Boogaloo

Cisco in an Hour 3: In 3-D

Cisco in an Hour IV: A New Hope

Cisco in an Hour V: for Vendetta

Cisco in an Hour VI: The Undiscovered Country

---
template: main

#### Socket

A connection between 2 programs using network protocols.
* This is usually between 2 computers, but does not have to be.

A socket corresponds to an IP (internet protocol) Address / Port pair.

To use a socket:
1. create the socket: `socket`
2. bind it to an address and port: `bind`
3. listen & accept/initiate a connection: `listen` `accept`, `connect`
4. send/receive data

---
template: main

#### Socket Protocols

__Stream Sockets (TCP)__
* Reliable 2 way communication.
* Must be connected on both ends.
  - 3 way handshake
* Data is received in the order it is sent.

__Datagram Sockets (UDP)__
* "Connectionless": an established connection is not required.
* Data sent may be received out of order (or not at all).
* Cannot use the usual `read` and `write` function calls.

---
template: main

#### Create a Socket

Functions and strcutres in `sys/socket.h`

`socket( domain, type, protocol )`
* Creates a socket, opens it like a file, returning a socket descriptor (int that works like a file descriptor)
* A socket is
* `domain`: type of address
  * `AF_INET` or `AF_INET6` or `AF_UNSPEC`
* `type`
  * `SOCK_STREAM` or `SOCK_DGRAM`
* `protocol`
  * Combination of domain and type settings
  * If set to 0 the OS will set to correct protocol (TCP or UDP)
* example: `int sd = socket(AF_INET, SOCK_STREAM, 0);`

---
template: main

`getaddrinfo` `<sys/types.h> <sys/socket.h> <netdb.h>`

* System library calls use a `struct addrinfo` to represent network addresses (containing information like IP address, port, protocol…)

* Will lookup information about the desired network address and get one or more matching `struct addrinfo` entries as a linked list.

`getaddrinfo(node, service, hints, results)`

* `node`: String containing an IP address or hostname to lookup
  * If `NULL`, use the local machine’s IP address (all of them).

* `service`: String with a port number or service name (if the service is in `/etc/services`)
* `hints`: Pointer to a `struct addrinfo` used to provide settings for the lookup
* `results`: Pointer to a linked list of `struct addrinfo` containing entries for each matching address.
* `getaddrinfo` will allocate memory for these structs, `freeaddrinfo` will release the entire linked list.

???
struct addrinfo
.ai_family
AF_INET: IPv4
AF_INET6: IPv6
AF_UNSPEC: IPv4 or IPv6
.ai_socktype
SOCK_STREAM
SOCK_DGRAM
.ai_flags
AI_PASSIVE: Automatically set to any incoming IP address.
.ai_addr
Pointer to a struct sockaddr containing the IP address.
.ai_addrlen
  Size of the address in bytes.


---
template: main

`bind( socket descriptor, address, address_length)` (server only)

* Binds the socket to an address and port. This allows a server has to have a set public* adrress and port.

* Returns 0 (success) or -1 (failure)

* `socket descriptor`: return value of socket

* `address`: pointer to a `struct sockaddr` representing the address.

* `address_length`: Size of the address, in bytes


* `address` and `address_length` can be retrieved from `getaddrinfo`.

---
template: main

#### Using Bind
```
//use getaddrinfo
struct addrinfo * hints, * results;
hints = calloc(1,sizeof(struct addrinfo));
hints->ai_family = AF_INET;
hints->ai_socktype = SOCK_STREAM; //TCP socket
hints->ai_flags = AI_PASSIVE; //only needed on server
getaddrinfo(NULL, “80”, hints, &results);  //Server sets node to NULL
//client: getaddrinfo(“149.89.150.100”, “9845”, hints, &results);

//create socket
int sd = socket(results->ai_family, results->ai_socktype, results->ai_protocol);

bind(sd, results->ai_addr, results->ai_addrlen);

//DO STUFF

free(hints)
freeaddrinfo(results);
```

---
template: main

`listen (socket_descriptor, backlog)` (server only)

* Set a socket to passively await a connection.

* Needed for stream sockets.

* Does not block.

* `socket descriptor`: return value of `socket`

* `backlog`: Number of connections that can be queued up.
  * Depending on the protocol, this may not do much.

---
template: main

`accept` (server only)

* Accept the next client in the queue of a socket in the listen state.
* Used for stream sockets.
* Performs the server side of the 3 way handshake
* Creates a new socket for communicating with the client, the listening socket is not modified.
* Returns a descriptor to the new socket
* Blocks until a connection attempt is made

---
template: main

`accept(socket_descriptor, address, address_length)`
* `socket descriptor`: descriptor for the listening socket
`address`: Pointer to a `struct sockaddr_storage` that will contain information about the new socket after accept succeeds.
* `address length`: Pointer to a variable that will contain the size of the new socket address after accept succeeds.

Using listen and accept
```
//use getaddrinfo (not shown)
//create socket
int sd = socket(results->ai_family, results->ai_socktype, results->ai_protocol);
//use bind
bind(sd, results->ai_addr, results->ai_addrlen);
listen(sd, 10);
int client_socket;
socklen_t sock_size;
struct sockaddr_storage client_address;
sock_size = sizeof(client_address);
client_socket = accept(sd,                                   (struct sockaddr *)&client_address, &sock_size);
```

---
template: main

`connect` (client only) <sys/socket.h> <sys/types.h>
Connect to a socket currently in the listening state.
Used for stream sockets.
Performs the client side of the 3 way handshake
Binds the socket to an address and port
Blocks until a connection is made (or fails)

connect (client only)
connect(socket descriptor, address, address length)
socket descriptor
descriptor for the socket
address
Pointer to a struct sockaddr representing the address.
address length
Size of the address, in bytes
address and address length can be retrieved from getaddrinfo()
Note that the arguments mirror those of bind()

Using connect
//create socket
int sd;
sd = socket(AF_INET, SOCK_STREAM, 0);
struct addrinfo * hints, * results;
//use getaddrinfo (not shown)
connect(sd, results->ai_addr, results->ai_addrlen);
