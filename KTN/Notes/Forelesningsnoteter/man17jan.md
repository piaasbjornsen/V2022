# Kap. 1
## 1.2 Network edge
* Et kommunikasjonsnettverk kan beskrives på forksjellige måter. Vi kan dele dem opp i forskjellige typer devices
* Eller vi kan zoome inn på deler av et nettverk og si noe om hva som befinner seg her.

* Network edge
  * Applications (e.g. web email)
  * Computing devices hosts = end system
    * Running network apps (e.g. PC, mobile, xbox)
* Communication links
  * Fiber optisk medium
  * Kopper
  * Radio
  * Satelitt
* Access network 
  * Physical media, wired
  * Wireless communication links
  * Ulike type egenskaper ulike medier har 
  * Viktig for at en bruker skal kunne koble seg til et nettverk 
  * Bredbånd
    * xDSL
    * Kabel-TV-nett
    * Fiber (som er den dominerende i Norge i dag)
* Newtwork core
  * Det er ingen brukere 
  * interconnected routers
  * network of network 
  * Her finner man
    * Rutere 
    * nettverk av nettverk 
* Routers
  * Hovedbyggeklossen i IP netverk
  * forward packedts (chunks of data)

    
## Network nodes are interconnected by a physical media
* Physical link
  * Between transmitter/reciver pairs
  * Poin to point vs. mulitpoint
  * Transmits bits 
* To typer linker
  * Guided media - wired
    * wierline signals propagate in solid media: copper, fiber, coax
    * Simple/duplex
  * Unguided media - wierless
    * No physical "wire": air, water, vaccum
    * Bidirectional 
    * Signals propagate freely in electromagnetic spectrum 
      * Reflection
      * obstruction by objects
      * interference 
    * Er ikke like godt/rask som guided media 
    * Har mange fordeler, mobilt 

## Home network  - Residential access network 
* Access point
* router
* firewall 
  * Beskytter
* NAT
  * Addresse oversettings funksjon 
* Wired Ethernet 

## Internet accesss through local area networks - Institustuinal accesss network
* Company/University ocal area network (LAN)
* Flere enheter som skal være koblet sammen
* Kanskje localservere 
* Routere som kan flytte 
* Ethernet: Mbit/s - Gbit/s

#1.3 Network core 
## Circuit switching end-to-end: No longer an alternative packet switching
* End-end resources reserved for "call" between source and destination
* Cuircuit segment idle if not used by call (no sharing)
* Commonly used in traditional telephone networks 

## The network core is a mesh of interconnecte routers
* Data sent in discrete "chunk" = packets
* Informasjonen som sendes, deles opp i små informasjonskomponenter (pakker), så blir det lagt på kontroll informajson, 
og så overføres hver enkelt IP pakke gjennom nettverket, uavhengig av hverandre.
* Packets are stored and forwarded from one router to the next, acreoss links on path from source to destination
* Each packet transmitted at full link capacity
  * L-bit packet intro link at R bps taked L/R seconds
* Internet is based on **packet switching**

## Internet struture: network of networks
* End system
  * Conntect to Internet via access ISPs (Internet Service Providers)
  * Residential, company and university ISPs
* Access ISPs
  * Must be ineterconnected
  * Resulting network of networks is complex
* Evolution was driven by economics ans national politica
* Nettnøytralitet
* ISPs har ikke lov til å diskriminere tjenester, og gi drpligere kvalitet til noen.

# 1.4 Packet-switched networks 

## Nettverksytelse - Hva forteller dette egentlig? 
## Throughput: the rate at which bits are transferred between sender and reciver 
* Throughput: Hvor mye data vi får mellom to noder som kommuniserer
  * Den ene veien kan være helt forksjellige fra den andre veien, og er helt uavhenige av hverandre 
* Server sends bits into pipe
* Unit: Bits per time
* Instantaneous: rate at given point in time
* Avergae: rate over longer period of time 

## Delay: FOure sources of packet delay
1. Nodal processing
   * check bit errors
   * determine output link
2. Queuing 
   * Time waiting at output link for transmission 
   * Depens in congestion level of router
3. Transmission
   * R = link bandwith (bit/s)
   * L = packet length (bits)
   * Time to send bits into link = L/R
4. Propagation
   * d = length of physical link
   * s = propagation speed in medium (2x10<sup>8</sup>)
   * propagation delay = d/s

## Packet loss: Packet arriving to full queue is dropped
* Queue (buffer) preceding link has finite capacity 
* Lost paclet may be retransmitted by a previous node, by source and system, or not at all
* Maximum throughouts is affected by Link speed/bandwidth, Round-trip time and Packet loss

## Cloud services - the more advanced the higher requirements on network performance

# 1.5 Protocol layers and service models 
## What's a protocal? - Protocols are used thourghout the internett
* Human protocols
  * What time is is? 
  * I have a question
* Network and end-to-end protocols
  * Between machines 
  * All communication activity in internet governed by protocols
* Protocols deine format, order og messages sent and recived amoge network entities, and actions taken on massage
transmission/recipt

## Many "pieces" make the network a complex structure but there is a structure to the design of the network: "layers"
* A protocol stack is the protocols of the variouse layers
* Application: supporting distributed applications
  * FTP, SMTP, HTTP
* Transport: process-process data transfer
  * TCP, UDP
* Network: Routing of datagrams from source to destination
  * IP, routing protocols
* Link: data transfer between neighboring network elements
  * PPP, Ethemet
* Physical: bits "on the wire" 
* 