Tags: [[networking]] [[network-protocols]] [[network-routing]]

# Routing
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42185996#overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
##### Routing Fundamentals
- for traffic between subnets or two networks
	- forwards traffic between subnets, internal and external networks, 2 external networks
- data frame comes from client device and goes to switch
- if switch ARP broadcast does not come back with any matches, it forwards the data frame to the router (default gateway)
- router will respond to ARP request from the original device on behalf of the destination device
	- original device will have the router's MAC address in it's ARP table for the destination IP
- router adds IP header to the data frame to make a packet (L3) and sends packet over to the router containing the destination
- that router now sends packet to switch and destination device on it's network
	- router strips off the IP header and adds the destination devices MAC address
		- router already knows the destination devices MAC
	- sends data frame to the switch that has the destination device connected
- Process is reversed to send data back to original device
##### Routing Tables
- helps determine which route is the best for a given packet
- route entries have a prefix, the longer, the more specific that network is
- 10.0.0.0 /8 is less specific than 10.1.1.0/24
	- /24 only 256 possible IPs
	- /8 16 million possible IPs
- entries also have the IP of the router on that network
- also the port used on the router to send to that route, and the cost

| DESTINATION NETWORK | NEXT ROUTER | PORT | ROUTE COST |
| ------------------- | ----------- | ---- | ---------- |
| 125.0.0.0           | 137.3.14.2  | 1    | 12         |
| 161.5.0.0           | 137.3.6.6   | 1    | 4          |
| 134.7.0.0           | 134.17.3.12 | 2    | 10         |
Routing Info Sources
Directly Connected Route
- If routers have direct cabling between them
Static Routes
- Configured by administrator
- hard set
- every router has a default route
	- 0.0.0.0/0
	- if the router does not know where to send the traffic, it sends here
Dynamic Routes
- found out by the device itself by exchanging info between routers
- if router 1 is connected directly to router 2 and router 3 (router 2 and router 3 are not connected)
	- router 2 wants to talk to router 3
	- because router 1 has a direct connection to router 2 and router 3, it can tell router 2 that to get to router 3, router 1 can forward it
	- router 2 will now update it's route table saying to go through router 1 to get to router 3
- finds the best route based on interface speed, amount of hops, etc.
	- based on dynamic routing protocol that is being used
![[routing-tables]] 
Loop Protection
- Split Horizon
	- prevents a route learned on an interface from being promoted out of the same interface
		- similar to STP
- Poison Reverse
	- rather than preventing the interface from promoting the route back out, it promotes it with a cost of Infinite
		- no other routers will ever want to use that as the cost will be higher than any other routes
##### Routing Protocols
###### Router Advertisement Methods
- how routers device to advertise and receive routes
Distance Vector
- amount of hops
- router sends a full copy of it's routing table to all directly-connected neighbors at set intervals
- slow convergence time
	- time it takes for all routers to update their tables when there is a topology change
Link State
- speed of links
	- uses Cost
- all routers need to know all paths to other routers
- faster convergence than Distance vectors
Hybrid
- combination of both
###### Interior Gateway Protocols
- communication between devices on an internal network
	- between subnets
- RIP (Routing Information Protocol)
	- uses distance vector 
	- updates every 30 seconds
	- slow convergence
	- UDP
- OSPF (Open Shortest Path First)
	- uses link state vector
	- fast convergence
- IS-IS (Intermediate System to Intermediate System)
	- uses link state vector
	- similar to OSPF, not as popular
- EIGRP (Enhanced Interior Gateway Routing Protocol)
	- uses both link state and distance vector
	- Cisco proprietary
	- more efficient than OSPF
###### Exterior Gateway Protocols
- used for communication between 2 separate networks
- BGP (Border Gateway Protocol)
	- uses path vector to determine least of amount of autonomous system hops, rather than router hops
		- more devices than just routers on the internet
	- used for backbone of the internet
	- very slow convergence

| ROUTING PROTOCOL | TYPE                     | INTERIOR/EXTERIOR |
| ---------------- | ------------------------ | ----------------- |
| RIP              | Distance Vector          | Interior          |
| OSPF             | Link State               | Interior          |
| EIGRP            | Advanced distance vector | Interior          |
| IS-IS            | Link state               | Interior          |
| BGP              | Path Vector              | Exterior          |

##### Route Selection
- believability of a route
- routers may support multiple interior gateway protocols
	- newer protocols are more believable
- Administrative Distance is the number that determines believability
	- lower the better
	- newer the route, lower the AD

| **ROUTING INFO SOURCE**  | **ADMINISTRATIVE DISTANCE** |
| ------------------------ | --------------------------- |
| Directly Connected Route | 0                           |
| Static Routes            | 1                           |
| EIGRP                    | 90                          |
| OSPF                     | 110                         |
| RIP                      | 120                         |
| External EIGRP           | 170                         |
| Unknown or Unbelieveable | 255                         |
##### Address Translation
###### NAT
- Translates private IP into a public IP
- used back when not many users on a network had to reach the internet at a given time
- Inside Local
	- private IP address of the device
- Inside Global
	- Public IP the device uses for the internet
	- router
- Outside Local
	- private IP of router
- Outside Global
	- Public IP of the destination device
DNAT (Dynamic)
- auto assigns IP address from a pool of addresses
- one-to-one translation
- can only have the amount of devices online as IP addresses in the pool
SNAT (Static)
- manually assign public IP addresses
- one-to-one translation
- can only have the amount of devices online as IP addresses in the pool
###### PAT
- one public IP address is used for multiple devices
- a random port gets added with the devices private IP address
##### Routing Redundancy Protocols
- Protocols that prevent disruptions by re-routing data if a path/device fails
- FHRP (First Hop Redundancy Protocol)
	- set of protocols that provide automatic failover to a backup router
	- use a virtual IP
		- that IP represents multiple devices
	- if one device goes down, clients don't need to update network configs
Hot Standby Router Protocol
- One router acts as the main router, with a secondary as backup
- if primary fails, secondary takes over
- Cisco only
Virtual Router Redundancy Protocol
- Similar to HSRP, but open protocol
Gateway Load Balancing Protocol
- Routers act together
- traffic is split between multiple routers
- if one goes down, others still work fine
- Cisco only