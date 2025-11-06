Tags: [[networking]] [[cloud]] [[network-routing]] [[high-availability]]
# Cloud and the Datacenter
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42186292#overview*
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
- 