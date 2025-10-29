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