Tags: [[azure]] [[azure-networking]] [[networking]] [[az-700]] [[dns]]

# Introduction to Azure Virtual Networks
### About
###### Author: *MSoft*
###### URL: *https://learn.microsoft.com/en-us/training/modules/introduction-to-azure-virtual-networks*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
### Explore Azure Virtual Networks
- fundamental building block of a private network in Azure
- Benefits from Azure's scale, availability and isolation
#### Capabilities of Azure Virtual Networks
- Allow resources in Azure to securely communicate with:
	- Internet
		- allow inbound or outbound to Internet via Public IPs or Load Balancer
	- Other Azure resources
		- securely and privately through VNets, VNet service endpoints, or VNet peering
		- connect to VMs and other Azure Resources like App Service Environment, Kubernetes Servcice, Virtual Machine Scale Sets, Azure SQL, Storage accounts, etc.
	- On Prem resources
		- Extend datacenter to the cloud through point-to-site, site-to-site VPNs, or Azure Express Route
- Filter traffic between subnets using NSGs or NVAs
- Route traffic between subnets, other VNets, on-prem networks and the internet by default
	- can create route tables to overwrite defaults
#### Design Considerations
##### Address space and subnets
- subscriptions can have multiple VNets
- Each VNet can have multiple subnets
###### Virtual Networks
- use RFC 1918 (private) addresses
	- 10.0.0.0 /8
	- 172.16.0.0 /12
	- 192.168.0.0 /16
- Some ranges are reserved and cannot be used
	- 224.0.0.0/4 (Multicast)
	- 255.255.255.255/32 (Broadcast)
	- 127.0.0.0/8 (Loopback)
	- 169.254.0.0/16 (Link-local)
	- 168.63.129.16/32 (Internal DNS)
###### Subnets 
- segmented range of IPs in a VNet
- must be a unique range to other subnets
- certain services require their own subnet
- useful for traffic management, security, etc.

### Configure Public IP Services
- Public IPs needed to talk to internet
- Dedicated to a specific resource in Azure
- Can be Dynamic (changes on resource stoppages/restarts) or static (remains the same)
- Can be basic or standard
	- Basic
		- basic or static
		- open by default
		- no availability zones, Routing preferences or global tier
	- Standard
		- static
		- secure by default
		- availability zones, routing preferences, global tier all supported
### Design Name Resolution for your VNet
- Azure has Public and Prvate DNS
#### Public DNS Services
- Azure public DNS is a hosting service for public domains using Azure global infrastructure
	- name servers all around the world, DNS requests route to the closest one
- Reliable, secure management of DNS without a separate solution
##### Configuration Considerations
- DNS zone names must be unique *within resource groups*
- The root domain/parent zone is registered at a domain registrar and pointed to Azure NS name servers
##### Delegate DNS Domains
- Azure is not a domain registrar itself
- Azure DNS zones allocate name servers from the Azure pool
- Parent domain can then be delegated to Azure DNS zone using the name servers
##### Child Domains
- Child zones can be used to create sub domains
- Can be in the same or a different resource group as the parent
#### Private DNS Services
- Azure managed  internal DNS service
	- Removed the need for a custom solution
- Use own custom domain rather than Azure provided ones
- Provides name resolution within a vNet and to connected networks
- 