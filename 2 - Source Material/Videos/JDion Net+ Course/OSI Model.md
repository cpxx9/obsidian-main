Tags: [[networking]]

# OSI Model
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42185566#overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
![[osi-model.png]]
- PDU (Protocol Data Unit)
	- Single unit of info transmitted in a network
	- named as L\<layer number\> PDU
		- L7 PDU is a layer 7 PDU 
	- Have specific names for layers 1-4
![[data.png]]
#### How data moves
- As data moved from Layer 7 to Layer 1
	- Data is encapsulated, a header is added at each layer
	- Layer 4 - Transport
		- TCP Header
		- Source and destination ports are added
	- Layer 3 - Network
		- IP Header
		- Source and destination IP addresses are added
	- Layer 2 - Data Link
		- Ethernet Header
		- Source and destination MAC addresses are added
	- Layer 1 - Physical
		- Layer 2 frames are sent as 1/0s
- As data moved from Layer 1 to Layer 7
	- Data is decapsulated
	- Layer 1 - Physical
		- Frames are put back together
	- Layer 2 - Data Link
		- Look for destination MAC on the switch, if not found, forward to router (L3)
	- Layer 3 - Network
		- Look for destination IP on the network, if not found, forward to default gateway
			- repeats until final host destination is found
	- Once host is found, data is decapsulated all the way up to L7 for application to use
