Tags: [[azure]] [[azure-networking]] [[networking]] [[az-104]] [[cloud]] [[network-routing]]

# Manage and control traffic flow in your Azure deployment with routes
### About
###### Author: MSoft
###### URL: https://learn.microsoft.com/en-us/training/modules/control-network-traffic-flow-with-routes/
###### Created:
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
- may want to have more control over the flow of traffic between the network
- possible with custom routes
	- user-defined routes or Border Gateway Protocol (BGP)
##### User defined routes
- 