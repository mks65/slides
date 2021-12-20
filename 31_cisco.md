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

Thicknet

* A single coaxial cable runs along the network.
* “Vampire taps” cut into the cable and connect to a computer.

.left[![vtap0](assets/l31_vtap0.png)]
.right[![vtap0](assets/l31_vtap1.png)]
