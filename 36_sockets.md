name: main

### .aim[Systems: Stop, Collaborate and Listen]
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
client_socket = accept(sd,(struct sockaddr *)&client_address, &sock_size);
```

---
template: main

`connect` (client only) `<sys/socket.h> <sys/types.h>`

* Connect to a socket currently in the listening state.

* Used for stream sockets.

* Performs the client side of the 3 way handshake

* Binds the socket to an address and port

* Blocks until a connection is made (or fails)

---
template: main

`connect(socket descriptor, address, address length)`
* `socket descriptor`: descriptor for the socket
* `address`: Pointer to a `struct sockaddr` representing the address.
* `address length`: Size of the address, in bytes
* `address` and `address length` can be retrieved from `getaddrinfo()`
* Note that the arguments mirror those of `bind()`

Using connect
```
//use getaddrinfo (not shown)
//create socket
int sd = socket(results->ai_family, results->ai_socktype, results->ai_protocol);
struct addrinfo * hints, * results;

connect(sd, results->ai_addr, results->ai_addrlen);
```
