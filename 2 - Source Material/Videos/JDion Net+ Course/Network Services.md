Tags: [[networking]] [[network-protocols]] [[network-routing]]

# Network Services
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42186078#overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
##### DHCP (Dynamic Host Configuration Protocol)
- Automatically configures network devices
- gives IP, subnet, gateway, and DNS server
- Central server is configured
	- Scope
		- address range
		- what Gateway to give, what subnet mask to give, what DNS servers to give
	- can have multiple scopes
##### SLAAC (Stateless Address Autoconfiguration)
- for IPv6 only
- does not require a central server like DHCP
- Device Initiation
	- device connects to network and creates temporary address (link-local, the second 64 bits of the IPv6 address)
- Router Solicitation
	- device sends message asking for any local routers to ID themselves
- Router Advertisement
	- routers will send back advertisement containing the network prefix (the first 64 bits of the IPv6 address)
- Address Configuration
	- Device will combine Network Prefix and the Link-Local address to create it's own IPv6 address
- Neighbor Solicitation
	- check and make sure no other devices on the network have the same address
##### DNS (Domain Name System)
- Converts host names to IP addresses
- Host File
	- simple text file on device that contains DNS to IP address list
- Local DNS Server
	- If configured, you can have a server on your LAN that controls DNS records
	- If device does not have entry in host file, will reach out to this server
	- usually configured for local devices only, set up to use a public DNS server (like Google) for any DNS records it does not know
	- DNS Cache
		- First time a client device tries to lookup a domain record, it will use the DNS server
		- Will then cache that records so it does not need to reach out to server every time you access that site in the future
		- TTL (Time to Live)
			- How long records can stay in cache
			- If client finds record in it's DNS cache, but the TTL has passed, it will reach out to the server again
- Public DNS server
	- same level as a local DNS server, but one you don't control
	- Most home networks use Google's Public DNS servers
		- 8.8.8.8 and 8.8.4.4
	- If device does not have entry in host file, will reach out to this server
	- Different levels of hierarchy
		- Google or your ISP DNS server may not have the DNS record stored
		- It will reach out to another DNS server at a higher level
		- Continues until DNS record is found, or Root Level is reached
- Root Level
	- Global organization controls the top level of all DNS records
	- .com, .net, .org, etc.
	- They keep records of all sites under these Top Level domains
###### Record Types

| **DNS RECORD** |  **DESCRIPTION**   |                     **FUNCTION**                     |
| :------------: | :----------------: | :--------------------------------------------------: |
|       A        |      Address       |            Links hostname to IPv4 address            |
|      AAA       |      Address       |            Links hostname to IPv6 address            |
|     CNAME      |   Canonical Name   | Points domain to another domain or subdomain (alias) |
|       MX       |   Mail Exchange    |            Directs emails to mail server             |
|      SOA       | Start of Authority |     Stores important info about a domain or zone     |
|      PTR       |      Pointer       |     Correlates and IP address with a domain name     |
|      TXT       |        Text        |                Adds text into the DNS                |
|       NS       |     Nameserver     |     Indicates which DNS nameserver has authority     |

##### NTP
- Synchronized clocks between systems
- many protocols rely on accurate time
- 15 tiers of hierarchy, or Stratums
	- Stratum 0
		- atomic clocks, other VERY precise time keeping devices
	- Stratum 1
		- NTP servers synced within microseconds of a Stratum 0 device
		- connected to other Stratum 1 devices to ensure they are synced
	- Stratum 2
		- connected and synced with multiple Stratum 1 servers
		- connected to other Stratum 2 devices to ensure they are synced
	- Stratum 3
		- same as stratum 3 but a level down
		- connected and synced with multiple Stratum 2 servers
		- connected to other Stratum 3 devices to ensure they are synced
	- this can continue down the hierarchy to wherever your device is
##### QoS
- Networks now carry voice, data, video, etc. traffic all on one network
- QoS allows you to configure priorities for traffic to ensure services run at the highest possible quality
###### Categorization
Best Effort
- Traffic is first in first out, no traffic re-shaping
Integrated Services (IntServ) Hard QoS
- traffic has strict bandwidth reservations
Differentiated Services (DiffServ) Soft QoS
- bandwidth reservations are dynamic and can change to meet the current network demands
	- web traffic may normally be set to 50% bandwidth, but a sale is going on and traffic is higher than normal, can go up to 60% or 70%
###### Mechanisms
Classification
- traffic is placed into categories based on the packet itself
Marking
- bits in the frame/packet are added to categorize traffic
Congestion Management
- Buffers extra traffic and releases from buffer based on priority of the traffic
- Queueing
	- example, VoIP is highest priority, then video, then web, then email
	- Weighted Fair
		- takes one packet from each type of traffic before taking the next packet of that same type
			- will send one VoIP, one, video, one web, one email, then repeat
		- not great for things such as VoIP traffic, as only one packet will be sent at a time, causing latency and jitter
	- Low Latency queuing
		- each type of traffic has priority
		- all traffic from higher priority is sent before moving to the next one
			- ALL VoIP packets, then ALL video packets, then ALL, web packets, then ALL email
			- if more VoIP comes in, that jumps to the top of the queue
		- can take very long for low priority traffic to get sent, causing more drops in that traffic
	- Weighted Round Robin
		- hybrid of other
		- each type of traffic has priority
		- instead of sending ALL traffic from higher priorities, a higher percent of traffic will be sent
			- 3 VoIP packets, 2 video packets, one web, one email, then repeat
		- Very good choice to maintain high QoS
Congestion Avoidance
- new packets are discarded if the output queue is already full
- RED (Random Early Detection)
	- used to prevent an outright overflow from occurring
	- if it notices the queue is getting full, it will start discarding traffic based on priority, rather than randomly
Policing and Shaping
- Policing
	- discards packets that exceed the rate limit
	- only good in very high speed connections
- Shaping
	- delays traffic that exceeds rate limit by holding in buffer
Link Efficiency
- compression
	- compress packets before sending
	- VoIP can be reduced by up to 50%
- Link Fragmentation and Interleaving (LF)
	- fragments large packets and interleaves smaller packets in between those fragments