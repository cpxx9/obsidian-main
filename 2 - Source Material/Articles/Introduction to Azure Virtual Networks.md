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
		- connect to VMs and other Azure Resources like App Service Environment, Kubernetes Service, Virtual Machine Scale Sets, Azure SQL, Storage accounts, etc.
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
- Available in all regions
#### Azure Private DNS Zones
- Internal resources only
- global, can be accessed from any region, subscription, VNet, or tenant
- highly resilient
	- replicated across all regions
	- aren't accessible via internet 
- can create custom Private Zones
	- configure specific DNS name
	- create records manually if needed
	- resolve names/IPs across zones/VNets
 
### Enable Cross-VNet Connectivity with Peering
- able to create connections between different parts of a virtual network infrastructure
- can be VNets in same or different regions
- network traffic between 2 peered VNets is private
	- on Microsoft backbone network
- networks appear as one
- Regional Peering - connects 2 VNets in the same region
- Global Peering - connects 2 VNets in different regions
##### Benefits of using virtual network peering
- low latency high bandwidth
- Able to use NSGs across VNets
- transfer data across networks, subscriptions, entra tenants, etc
- no downtime required to peer
#### Configure VNet Peering
- create 2 VNets
- Peer the VNets
- Create resources in each VNet
- Test communication between the 2
##### Gateway Transit and Connectivity
- Can configure VPN to be a gateway transit point
	- peered networks use the gateway to access other resources
- VNets can only have one gateway
- allows the VNet to communicate with resources outside of the peering
	- use site-to-site VPN to connect to on-prem
	- connect to another VNet
	- use point-to-site to connect to client
- gateway transit allows peered VNets to share the gateway
	- only need one VPN in peered VNets
	- all VNets get access to resources in on the gateway (on-site, etc.)

### Implement Virtual Network Traffic Routing
- route tables are auto generated  for each subnet in a VNet
	- default routes, as well as UDRs
#### System routes
- the default routes created by azure for each subnet
- cannot be edited or removed
	- can be overridden
- optional default routes may be provided if using specific Azure capabilities
##### Default system routes
- each route contains an address prefix and next hop type

| Source  | Address        | Next     |
| ------- | -------------- | -------- |
| Default | Unique to VNet | VNet     |
| Default | 0.0.0.0/0      | Internet |
| Default | 10.0.0.0/8     | None     |
| Default | 172.16.0.0/16  | None     |
| Default | 192.168.0.0/16 | None     |
| Default | 100.64.0.0/10  | None     |
- next hop types:
- **VNet** - routes traffic between address ranges withing a VNet, default is how different subnets talk to each other
- **Internet** - Routes traffic to the internet, default routes all traffic to an address not in the VNet address range to the internet
	- excludes Azure services, as those are routed over the MSoft backbone network
- **None** - Traffic is dropped
##### Optional default system routes
- Azure adds default system routes for any Azure capabilities enabled
	- either to specific subnets, or all subnets depending on the capability

| Source                  | Address prefixes                         | Next hop type                 | Subnet within virtual network route is used |
| ----------------------- | ---------------------------------------- | ----------------------------- | ------------------------------------------- |
| ******                  | ******                                   | ******                        | ******                                      |
| Default                 | Unique to VNet                           | Virtual network peering       | All                                         |
| Virtual Network Gateway | Prefixes advertised from on-prem via BGP | All                           |                                             |
| Default                 | Multiple                                 | VirtualNetworkServiceEndpoint | Only the subnet the service is enabled for  |
- **VNET peering** - routes  generated for each address range between 2 peered VNets
- **Virtual** **network gateway** - Azure adds one or more routes when VNet gateway is added
- **VirtualNetworkServiceEndpoint** - Azure adds the public IP address(es) for certain services when you enable it's service endpoint
	- Service endpoints are enabled for individual subnets within a virtual network, so  routes are only added for that subnet 
	- Azure updates these routes as the IPs change
#### User defined routes
- Default routes can be overridden with UDRs
- each subnet can have one or more route table
	- when created and applied to a subnet, the UDRs combine or override the default routes
- Next hop types:
	- **Virtual Appliance** - a VM that usually runs a network application (firewall)
		- need to specify next hop IP
	- **Virtual network gateway** - used to route traffic through a VNet gateway
	- **None** - used to drop traffic
	- **Virtual Network** - used to override defaults routes within VNet
	- **Internet** - Routes traffic to the internet
#### Consider Azure Route Server
- simplifies dynamic routing between NVA (Network Virtual Appliance) and VNet
- automatically updates routing tables on NVA whenever VNet addresses change
- automatically updates UDRs when NVA announces new routes, or withdraws old
- can peer multiple instances of NVA to Azure Route Server
- uses on BGP, a common protocol, to interface between NVA and Azure Route Server
- can be deploying in any new/existing VNet
#### Troubleshoot with effective routes
- View routes that are currently effective for any network interface in your VNet

### Configure Internet Access with Virtual NAT
- Azure NAT lets internal resources in VNet share a routable public IPv4 address
- Can map traffic flow from subnets through Virtual NAT
- No UDRs needed
	- NAT takes precedence over other outbound routes, replaces default internet destination of a subnet
- supports up to 16 public IP addresses
	- Load balancer, Public IP address, Public IP prefix
#### Limitations of NAT
- does not work in IPv6
- cannot span multiple VNets
- does not support IP fragmentation

