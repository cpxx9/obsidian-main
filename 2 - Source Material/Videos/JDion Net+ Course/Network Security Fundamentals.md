Tags: [[networking]] [[network-security]] 
# Cloud and the Datacenter
### About
###### Author: *Jason Dion*
###### URL: *https://ctcomp.udemy.com/course/comptia-network-009/learn/lecture/42186388#*overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
##### Cloud Connectivity
VPN
- cheaper 
- site-to-site VPN to the cloud
Private-Direct
- more expensive
- higher speeds, better performance, better security, better redundancy
- Azure Express Route, Amazon Direct Connect
##### Cloud Security
- VPC - Virtual Private Cloud
Subnet
- Public or private
Route Tables
- determine where traffic within the VPC with be directed
Internet Gateway
- allows connectivity between VPC and Internet
NAT Gateway
- allow instances in private subnet to connect to internet or other cloud services
- prevents Internet from initiating a connection with those instances
Network ACL (Access Control List)
- simple firewall rules, inbound or outbound
- stateless, does not care about what comes before or after
Security Group
- like a stateful firewall
VPC Peering
- enables routing between two VPCs privately
VPC Endpoints
- Allow private connection to services in AWS/Azure without using Internet Gateway, VPN, or direct connection
##### Network Function Virtualization (NFV)
- traditionally routing, firewalls, Load balancing, IDS/IPS are all separate hardware devices
- Extracts hardware functions in to software applications that can be installed on normal servers
- VNF - Virtual Network Functions
- Flexible, rapid deployments
- Cost efficient
- may be more complex
NFVI (NFV Infrastructure)
- contains the hardware and virtual resources (servers) needed to deploy VNFs
MANO (Management and Network Orchestration)
- oversees lifestyle management of the VNFs
- orchestrates resources across the NFVI
VNFs
- actual software implementations of the network functions
##### Software Defined Networking (SDN)
- using software based controllers or APIs to communicate with hardware infrastructure and direct traffic on a network
Control Plane
- responsible for carrying traffic to and from router
- decides how traffic is prioritized and where it should be switched to on the network
- switches, routers, QoS device rules
Data Plane
- carries user traffic 
- bulk of traffic
- switching and routing occurs here
- control plane decides how traffic moved, data plane actually moves it
Management Plane
- administers network devices
- monitors traffic
##### SD-WAN
- Virtualized approach to managing and optimizing WAN connections
	- efficiently route traffic between remote sites, datacenters, and cloud environments
- allows enterprises to leverage any combination of transport services to connect users to applications
- managed entirely in software
	- layer over many types of network transport (mpls, microwave, cable, etc.)
- uses centralized control function to route traffic accross the WAN
- typical WAN would use hub and spoke, all data from sites routes through main office
	- SD-WAN intelligently routes traffic (internet straight to internet, internal traffic to main office/cloud, etc.)
	- provides better user experience, better speeds
	- offers management of this traffic even though it never passes through main office
##### VXLAN ( Virtual Extensible Local Area Network)
- addresses limitations posed by traditional VLANs
	- More scalable
		- only 4096 potential IDs in VLANs
	- More flexible
		- can extend layer 2 networks across datacenters
- Network overlay technology
	- encapsulates ethernet frames within a UDP packet
	- extends layer 2 network over layer 3 infrastructure
	- virtual layer 2 network that can span physical layer 3 networks
	- enables large number of virtual networks across physical ones
- encapsulates layer 2 ethernet frame within a layer 3 UDP packet
	- 24bit network identifier, VNI
		- 16 million
- VXLAN Tunnel Endpoint
	- perform the encapsulation and de-encapsulation
	- usually within a hypervisor, or physical switches
- VXLAN Segment
	- layer 2 network overlayed onto layer 3 network
	- identified by the 24bit VNI
- Devices on the same VXLAN segment can communicate with others on the same VXLAN, regardless of physical location
- Challenges
	- complexity when configuring
	- latency caused by encapsulation and de-encapsulation
	- require multicast traffic support
##### SASE (Secure Access Secure Edge) and SSE (Security Service Edge)
- Provide secure fast and reliable access to cloud based resources, regardless of where users are
- SASE
	- consolidates numerous WAN and security functions into a single cloud-native service 
	- allows secure and reliable access, regardless of where users are
	- addresses challenges in securing and connecting users and data across multiple locations (branch offices, cloud, mobile devices)
	- SDN to provide networking from the cloud rather than physical devices
		- Firewall, VPN, Zero-trust network access, cloud access security brokers
- SSE
	- aspect of SASE, focusing on the security services
	- ensures security of devices outside of traditional corporate controls (mobile, byod, etc.)
	- Secure Web Gateways
		- inspect and filter traffic from web/internet for malware
	- Cloud Access Security Brokers
		- border device between cloud service consumers and providers
		- monitors activity and enforces security policies
	- Zero Trust Network Access
		- Designed not to trust any user or device, inside or outside the network by default