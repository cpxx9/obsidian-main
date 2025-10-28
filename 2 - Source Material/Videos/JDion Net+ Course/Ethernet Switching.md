Tags: [[networking]] [[network-routing]]

# Ethernet Switching
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42185860#overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
#### Ethernet Fundamentals
History
- Coax 
	- BNC and Vampire Taps
	- Thin-Net
		- 10Base2
		- thinner coax cable
		- 200 meter range
	- Thick-Net
		- 10Base5
		- thicker coax cable
		- 500 meter range
- Twisted Pair
	- 10Base-T
		- 10 Mbps
		- 100 meter range
Network Access Styles
- Deterministic
	- network access is very organized and orderly 
	- each device needs to wait its turn to transmit data
		- electronic token is given to show it is that device's turn
		- one main device is the moderator
	- no collisions
- Contention Based
	- network access is not as organized
	- each device that transmits data will look for an opening where no data is transmitted
		- if another device is already using that channel, it will wait and try again
	- collisions occur
	- much more efficient use of network resources
CSMA/CD (Carrier Sensing Multiple Access w/ Collision Detection)
- Carrier Sensing
	- listen to network and determine if there is already a signal being transmitted
- Multiple Access
	- Many devices all able to access/listen on the network at a same time
- Collision Detection
	- if a collision is detected, each device with come up with a random backoff timer
		- device will pick random amount of time, and then try to re-transmit after that time
- More devices on each network segment means more collisions
	- each segment is a Collision Domain
	- Each cable in the network or a hub (no matter how many devices connected) is a single Collision Domain
		- devices on a hub run on half-duplex, can only transmit or receive at once, not both
	- each port on a switch is its own Collision Domain
#### Network Devices
Hub
- L1 Device
- connects multiple network segments together (multiple devices)
- passive
	- repeats signal with no amplification
- active
	- repeats hub and boosts signal
	- allows running twisted-pair cable more than 100m
- smart
	- allows login for remote management (SNMP)
- one Collision Domain for all devices connected
Bridge
- L2 device
- analyze source MAC addresses to make smart forwarding decisions based on the destination MAC
Switch
- L2 device
- Hub and Bridge combined
- single broadcast domain
Router
- L3 device
- connects multiple networks and makes forwarding decisions based on network info
	- IPv4/IPv6
- can combine multiple network types
	- coax/ethernet, ethernet/fiber, fiber/coax, etc.
- routers can separate broadcast domains
- there are now L3 switches
	- can do routing decisions based on IP like routers
	- each port is it's own Broadcast Domain and own Collision Domain
	- not as good at routing as routers are
		- good for smaller business with smaller networks
#### VLANs
- Logical subdivision of a network
- creates separate Broadcast Domains
- allows logical grouping of devices even if on different network switches
- switch configured with VLANS will tag data frames with a VLAN ID 
- other switches will read that frame and know what path to send data
- Enhance security
	- networks are segmented so sensitive data can be isolated
	- data needs to pass through routers/L3 switches to get to another network segment
		- ACLs can be used at each point to dictate what types of traffic can leave/enter a VLAN
- Improve Performance
	- reduces the size of Broadcast Domains
		- decreases the amount of traffic being sent over each network segment
- Increased Management
	- Can implement policy changes or troubleshoot issues more granularly
- Improved Cost Efficiency
	- less need for physical switches
- Switch Virtual Interface (SVI)
	- Allows switches to route traffic between different VLANs without needing a router
	- makes the switch L3
###### VLAN Configuration
802.1Q Tagging
- IEEE standard
- Adding VLAN tag to data frames
- trunking
	- separate/secure transmission of data across VLANs
Native VLAN
- default VLAN used for traffic that comes in untagged
- useful for legacy devices without VLAN capabilities
- must be a consistent VLAN ID across all network devices
Voice VLAN
- VLAN used specifically for VoIP traffic
- VoIP traffic is very sensitive to packet loss
- keeps voice traffic separate from other network traffic
	- can set QoS policies to prioritize traffic on the Voice VLAN
	- improved quality in calls
Link Aggregation
- Logical combination of multiple network connections to a single link 
- gives higher bandwidth and redundancy
	- can take 4 1 Gbps connections and combine to make a 4Gbps bandwidth link
		- useful for trunk ports on switches
	- if one goes down, still have 3 1Gbps connections making 3 Gbps bandwidth
Speed/Duplex
- Half-Duplex
	- send or receive data at one time
- Full-duplex
	- send and receive data at one time
- Auto-negotiation
	- auto-select highest settings the two devices they have in common
	- can sometimes be wrong, best to manually configure
#### Spanning Tree Protocol (STP) 802.1d
![[STP-model]]
- allows redundant links between switches
- prevents network loops
How a loop happens
- traffic has multiple paths to follow
- one switch gets mac address from arp replies on multiple interfaces from multiple switches
- this switch then broadcasts back out on those multiple interfaces
- this fills the MAC address tables on switches with the same MAC address for multiple interfaces
- traffic now does not know where to go as a circle is formed
- creates a Broadcast Storm of traffic being forwarded back and forth between the switches, duplicating and never getting to it's destination
	- keeps duplicating until network fully crashes
	- only way to fix is unplug switch and wait for data to be lost on the network
How STP prevents loops
- Cost
	- speed of network connection
	- higher speed, lower cost
- Root Bridge (switch)
	- acts as reference point for the entire spanning tree
	- switch with the lowest BID (Bridge ID)
		- made of Priority value and MAC address
			- priority is comes from Cost 
			- if priority is the same, lowest manufacturer MAC address is priority
- Non-Root Bridge (switch)
	- all other switches in the spanning tree
- Root Port
	- every non-root bridge has a single root port
	- closest to the root bridge in terms of Cost (speed of network connection)
		- if Cost is equal, goes by lowest switch port
- Designated Port
	- Every network segment has at least one designated port
		- closest port to the root bridge in terms of Cost
	- Every port on a Root Bridge are Designated ports
- Non-Designated Port
	- ports that block traffic to stop loops
	- all ports on Non-Root bridge that are not the Root Port
	- receive data as BPDUs (Bridge Protocol Data Units), but do not forward it
	- if a link goes down, the Non-designated port will detect failure and transition to Designated or Root Port if needed
#### Network Access Control (NAC)
#### Maximum Transmission Unit (MTU)