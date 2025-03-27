Tags: [[azure]] [[azure-networking]] [[networking]] [[az-104]] [[cloud]]

# Configure Azure Virtual Network peering
### About
###### Author: MSoft
###### URL: https://learn.microsoft.com/en-us/training/modules/configure-vnet-peering/
###### Created:
-------------------------------------------------------------------
## Notes
Peering provides secure communication between virtual networks.
### Determine Azure Virtual Network Peering uses
- after peering, two networks act as one
##### Things to know
- can be regional or global
- after peering, networks are still managed as separate resources
##### Things to consider
- traffic between peered networks is private
	- kept on Azure backbone network
- high performance, low latency
- easy set up
- no downtime to set up
### Determine gateway transit and connectivity
- can set up Azure VPN gateway as a transit point
##### Things to know about Azure VPN Gateway
- each vNet can only have one VPN gateway
- regional and global
- allows peered network to share the gateway for access to external resources
	- do not need a VPN in each vNet
- can apply NSGs
### Create virtual network peering
can configure using PowerShell, Azure CLI, or the Azure Portal
##### Things to know
- need at least 2 vNets
- second vNet is called the _remote network_ 
- resources on 2 vNets cannot communicate with each other unless peering is set up
- Can check status of peerings in the portal
### Extend peering with user-defined routes and service chaining
- peering is non-transitive
	- peer networks A and B, peer networks B and C, networks A and C _can not_ communicate
- need to use other methods to extend
##### Things to know about extending peering
- methods include hub and spoke networks, user defined routes, service chaining
- can implement multi-level hub and spoke with these methods
- hub and spoke
	- hub vNet can have the infrastructure components, VPN, NVA, etc.
	- all spoke vNets can peer with the hub vNet
- User-defined route (UDR)
	- peering allows the next hop in a UDR to be an IP of a VM in the peered vNet, or a VPN gateway
- Service chaining
	- used to direct traffic from one vNet to a virtual appliance or gateway

