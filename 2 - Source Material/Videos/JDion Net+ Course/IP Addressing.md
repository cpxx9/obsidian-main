Tags: [[networking]] [[physical-networking]]

# IP Addressing
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42185916#overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
#### IPv4 Addressing
###### Classes
- determined by first Octet in IPv4
A
- 1-127
- Default Mask: 255.0.0.0
	- /8
- 16.7 million possible hosts
B
- 128-191
- Default Mask: 255.255.0.0
	- /16
- 65,546 million possible hosts
C
- 192-223
- Default Mask: 255.255.255.0
	- /24
- 256 possible hosts
D
- 224-239
- Default Mask: none
- They are reserved for multicast routing
- Multicast address
	- logical identifier for a group of hosts in a network
	- data sent to these IPs will be send to all hosts in that group
E
- 240-255
- Default Mask: none
- 268 million possible hosts
- reserved for experimental research/development
###### Subnetting
- dividing network into smaller portions
Classful
- one that uses the default for the IP's  class
	- if a Class C IP, will be 255.255.255.0
Classless
- Borrows host bits from IPv4 address for the network bits
- If a Class C IP, could be 255.255.255.192
	- takes 2 bits from the host part of the address and adds to network part
CIDR (Classless Inter-Domain Routing)
- use a /x with x being the amount of network bits
- 192.168.1.4/24
	- subnet is 255.255.255.0 (24 network bits)
- 192.168.1.4/26
	- subnet is 255.255.255.192 (26 network bits)
###### Types
Public
- Unique IP assigned to each device on the Internet
- Managed by ICANN
Private
- not accessible over the internet
- used for LAN devices
- 10.x.x.x, 172.16-31.x.x, 192.168.x.x
- uses NAT to allow talking out on the internet
	- allows single device (router) to translate private IP addresses to a single public IP and port
Loopback (Localhost)
- 127.x.x.x
- Really only use 127.0.0.1
- Routes traffic back to same device
- used for troubleshooting/testing
APIPA
- Automatic Private IP Address
- 169.254.x.x
- Operating System assigned address if DHCP assignment fails
- stops system from constantly making DHCP requests if they continue to fail
###### Data Flows
Unicast
- Data flows from single source to single destination
Multicast
- Data flows from single source to multiple destinations
Broadcast
- Data flows from single source to all destinations
###### Assigning
Static
- Manually input IP, subnet, gateway, DNS servers
- not practical in large networks
Dynamic
- server set up to assign IP
- DHCP (Dynamic Host Configuration Protocol)
- can set specific pool of IPs to be used
- will lease out IPs, if a device disconnects that IP will now be available again
##### Subnetting
- splitting a larger network into smaller ones
10.0.0.0 /8
- would have 16.7 million IPs
- can be split to smaller groups
- 10.0.0.0 /24
	- 256 IPs
- 10.0.1.0 /24
	- 256 IPs
- 10.0.2.0 /24
	- 256 IPs
![[Subnet-Cheat]]
#### IPv6 Addressing
- 128 bits of space
- 64 bits is the network portion, 64 bits is the host portion
- more efficient than IPv4
	- no broadcast traffic
- more secure
	- no fragmentation
	- no MTUs
- simplified header
	- 5 fields instead of 12 like IPv4 has
- 8 segments of 4 hexadecimal digits
	- 32 digits total
	- 0-9, A-F
Short Hands
- continuous zeros can be simplified as just one zero in each section
	- 2018:0000:0000:0000:0000:0000:4815:54AE
	- 2018:0:0:0:0:0:4815:54AE
- continuous zeros across segments can be simplified with double colon
	- can only be used once in an address
	- 2018::4815:54AE
##### Address Types
- single interface can have multiple IPv6 addresses
	- can be combination of the following types
Unicast
- single interface
- globally-routed
	- start with 2000-3999
	- used on public internet
- Link-local
	- start with FE80
	- private IPv6 addresses
	- SLAAC (Stateless Address Autoconfiguration)
		- see below
Multicast
- starts with FF
- identifies a set of interfaces to send packets to
Anycast
- identifies a set of interfaces so a packet can be set to any member of a set
- allocated from unicast address space
##### SLAAC (Stateless Address Autoconfiguration)
- host does not need to get address configuration from central server
- assigns itself a unique Link-local address when connected to network based on MAC address
- tests the uniqueness
- contact the router
- provide direction to the node on how to proceed with autoconfiguration
- configure global Unicast address it would like to use
EUI (Extended Unique Identifier)
- assigns unique 64 bit IPv6 interface identifier called EUI-64
- uses MAC address
	- 48 bit address 
	- split into 2 portion (OUI and NIC)
- add FF into the middle of the 2 MAC address portions
	- 00:21:2F:B5:6E:10
	- 00:21:2F:FF:FE:B5:6E:10
- this gives us the 64 bit host portion of the IPv6 address
- combine with the 64 bit network portion to get entire globally-routed unicast IPv6 address
	- device uses auto-discovery (SLAAC) to determine the network portion
NDP (Neighbor Discovery Protocol)
- used to determine layer 2 addresses that are on a network
	- router solicitation/advertisement, neighbor solicitation/advertisement and redirection
- pick host ID based on others'
##### Data Flows
Unicast
- send data from one source to one destination
Multicast
- send data from one source to multiple destinations
Anycast
- send data from one source to the device nearest to multiple (specific) destination devices
- allows for efficient updates of routing tables
- determines which gateway is closest to the host, and then communicate with it over Unicast
	- gateway then uses Anycast to all other hosts in a group 
	- finds the next closest gateway and updates that routing table
	- continues until all routing tables are updated
	- original gateway does not need to keep sending out the data
##### Backwards Compatibility with v4
Dual Stack
- allows coexistence of IPv4 and v6 on the same network infrastructure
- all network devices (routers, switches, hosts) are configured with v4 and v6
- devices prefer IPv6 and fallback to v4 if needed
- if DNS query returns AAAA and A records, it will try v6 first
Tunneling
- allows 2 IPv6 devices to communicate through a v4 network
	- v6 packets are encapsulated within IPv4 packets
	- sent across v4 infrastructure 
	- arrive at v6 destination and are de-capsulated
NAT64
- allows v6 only devices to talk with v4 only devices
- translates v6 addresses to v4 addresses and back
- gateway device at the end of a v6 network that translates all traffic through it to v4
	- multiple v6 devices share a same IPv4 address