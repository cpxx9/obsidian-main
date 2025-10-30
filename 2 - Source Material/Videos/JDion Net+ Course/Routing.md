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
###### Internal
- communication between devices on an internal network
	- between subnets
###### External
- used for communication between 2 separate networks