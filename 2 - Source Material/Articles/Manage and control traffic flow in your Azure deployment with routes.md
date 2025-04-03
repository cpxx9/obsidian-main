Tags: [[azure]] [[azure-networking]] [[networking]] [[az-104]] [[cloud]] [[network-routing]]

# Manage and control traffic flow in your Azure deployment with routes
### About
###### Author: *MSoft*
###### URL: *https://learn.microsoft.com/en-us/training/modules/control-network-traffic-flow-with-routes/*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
Azure makes it easy to control the flow of traffic within and between vNets
Custom routes can be used to specify exactly how traffic flows

### Identify routing capabilities of an Azure virtual network
#### Azure routing
- Azure has default routes that determine the way traffic is routed across subnets, vNets, and on-premise networks
	- Cannot be deleted, but can be overridden by adding custom routes
- Default system routes:

| Address prefix |  Next Hop Type  |
| :------------: | :-------------: |
| Unique to vNet | Virtual network |
|   0.0.0.0/0    |    Internet     |
|   10.0.0.0/8   |      None       |
| 172.16.0.0/12  |      None       |
| 192.168.0.0/16 |      None       |
| 100.64.0.0/10  |      None       |
- Next hop types
	- Virtual network, prefix represents address range created at the virtual network level
	- Internet, the default routes any address range to the internet, unless overridden with another one
	- None, traffic sent to these routes is dropped. Creates 3 private IP ranges
- Other system routes get created if any of the following are enabled
	- Virtual network peering
	- Service chaining
	- Virtual Network Gateway
	- Virtual network service endpoint
##### Virtual network peering and service chaining
- let Azure vNets connect to one another
- same region or across regions
- Default routes get created to allow this communication
- Service Chaining allows overriding these routes via custom routes
##### Virtual network gateway
- sends encrypted traffic between Azure and on-prem, over the internet
- send encrypted traffic between Azure vNets
##### Virtual network service endpoint
- direct connection between Azure resources
- used to allow traffic flow only from private VMs
#### Custom routes
- system routes are nice to get up and running easily
- may want to have more control over the flow of traffic between/within networks
- possible with custom routes
	- user-defined routes or Border Gateway Protocol (BGP)
##### User defined routes
- override default system routes
- example: network with 2 subnets. add a NVA for a firewall
	- can create user defined route to ensure all traffic between the subnets gets routed through the firewall first
- can specify the next hop type in the UDR
	- Virtual appliance, usually a firewall or other network device used to analyze/filter traffic, or a load balancer
	- Virtual network gateway, routes traffic to a virtual network gateway, VPN
	- Internet, routes traffic out to the internet
	- None, drops traffic
##### Service tags for user defined routes
- can use a service tag as the address prefix rather than a specified address or range
- represents a group of IP address prefixes from an Azure service
- Azure manages the addresses of services encompassed in the service tag
	- automatically update
	- no need to manually stay on top of and update user defined routes
##### Border gateway protocol
- standard routing protocol for exchanging routing info between networks
	- transfers data and info between systems such as host gateways
- can be used to exchange routes between an on prem and virtual Azure network gateway
- Can be used with Azure ExpressRoute or Site-to-Site VPN
#### Route selection and priority
- if multiple routes are available, the one with the longest prefix match gets priority
- Example, traffic to 10.0.0.2, routes available for 10.0.0.0/16 and 10.0.0.0/24
	- 10.0.0.0/24 wins, as it is more specific, e.g. longer
- if there are multiple routes with the exact same prefix, priority as follows
	1. User defined routes
	2. BGP routes
	3. System routes

### Create custom routes
#### Create Route Table
**Create route table**
```powershell
az network route-table create \
	--name <name> \
	--resource-group "resource group name" \
	--disable-bgp-route-propagation false
```
*example:*
```powershell
az network route-table create \
	--name publictable \
	--resource-group "[sandbox resource group name]" \
	--disable-bgp-route-propagation false
```
**Create route**
```powershell
az network route-table route create \
	--route-table-name <name> \
	--resource-group "resource group name" \
	--name <name> \
	--address-prefix <address/mask> \
	--next-hop-type <type> \
	--next-hop-ip-address <address>
```
_example:_
```powershell
az network route-table route create \
	--route-table-name publictable \
	--resource-group "[sandbox resource group name]" \
	--name productionsubnet \
	--address-prefix 10.0.1.0/24 \
	--next-hop-type VirtualAppliance \
	--next-hop-ip-address 10.0.2.4
```
#### Associate route table with subnet
_You must have a subnet already created that you can assign the route table to_
Associate table with subnet
```powershell
az network vnet subnet update \
	--name <name of subnet already created> \
	--vnet-name <name of vnet> \
	--resource-group "resource group name" \
	--route-table <name of table>
```
_example:_
```powershell
az network vnet subnet update \
	--name publicsubnet \
	--vnet-name vnet \
	--resource-group "[sandbox resource group name]" \
	--route-table publictable
```

### What is an NVA
- Network Virtual Appliance is a VM consisting of various layers
	- firewall
	- WAN optimizer
	- application-delivery controllers
	- routers
	- load balancers
	- IDS/IPS
	- proxies
- Many providers available in the Azure Marketplace
	- Cisco, Check Point, Barracuda, Sophos, WatchGuard, Sonicwall, etc.
- Some uses
	- filter inbound traffic to vNet, block malicious requests, block requests from unaccepted resources
#### Network virtual appliance
- VMs that control the flow of traffic by controlling routing
- Typically used for managing traffic flowing from a perimeter network to other networks/subnets
- Firewalls can be used in multiple ways
	- can create a perimeter subnet in the vNet that the firewall resides in
	- can use micro segmentation
		- create dedicated subnets for the firewall, and deploy other services to separate subnets
		- all traffic gets routed through the firewall subnet and is inspected at layer 4 or layer 7 
			- depends on the NVAs deployed within the firewall subnets
##### User-defined routes
- Default system routes may be enough to get the environment up and running
- UDRs let you more closely manage the flow of traffic
#### NVAs in a highly available architecture
- If all traffic is being routed through an NVA, it becomes a single point of failure
- important to make sure NVA deployments are highly available