name: main

### .aim[Systems: Cisco in an Hour™]
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
</style>

---
template: main

#### Layer Models of Networking

Due to the complexity of network communications, the topic is often conceptualized into distinct layers so people can work on specific components rather than everything at once.

--

The bottom layer is the most concrete, with each subsequent layer becoming more abstract (relying less on the physical connections and more on code).

--

There are various competing models, including the OSI (Open Systems Interconnections) and TCP/IP Models.

--

TCP/IP Model Layers
1. Application
2. Transport
3. Internet
4. Link

---
template: main

#### Link Layer

Point-to-point transmission between devices on the same (local) network.

--

Combines physically connecting computers with basic addressing and transmission protocols.

--

Physical connection

* How to transmit bits between two computers.

--

* Electrons, photons, radio waves…

---
template: main

#### Link Layer: A brief history of physical connections

__Thicknet__

A single coaxial cable runs along the network.

“Vampire taps” cut into the cable and connect to a computer.

![vtap0](assets/l31_vtap0.png)] ![vtap1](assets/l31_vtap1.png)]

---
template: main

#### Link Layer: A brief history of physical connections

__Thinnet__

A single coaxial cable runs along the network.

T-Connectors connect computers to the main cable.

.center[![tcon](assets/l31_tconnect.png)]

---
template: main

#### Link Layer: A brief history of physical connections

__Thin/Thicknet network topology__

.center[![topology](assets/l31_think-thin.png)]

???
Each new computer degrades the network
collisions could cause issues

---
template: main

#### Link Layer: A brief history of physical connections

__Token Ring__

Each computer is connected in a ring to each other.

Only one computer has command of network resources at a time. This is called "having the token”.

The network sends a "token" throughout the ring, which contains the identity of the computer allowed to use the network. All other computers must wait to use the network.

.center[![token](assets/l31_token.png)]

---
template: main

#### Link Layer: A brief history of physical connections

__Ethernet__

Multiple computers connect to a single hub or switch.

Hub
* Broadcasts the data to all the computers

Switch
* Sends data to a specific computer

.center[![token](assets/l31_token.png)]
