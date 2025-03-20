Tags: [[azure]] [[azure-networking]] [[networking]] [[az-104]] [[cloud]]

# Configure Network Security Groups
##### Author: MSoft
###### URL: https://learn.microsoft.com/en-us/training/modules/configure-network-security-groups/
###### Created:
-------------------------------------------------------------------
## Notes
NSG = Network Security Group
AZP = Azure Portal
### Implement NSGs
- limit traffic to resources in v network via rules assigned to the group
- assign to subnet or interface
##### Things to know
- list of security rules that allow/deny inbound/outbound traffic
- can be associated to a subnet or network interface
- can be associated multiple times
- create groups, assign rules to groups, and assign groups to VMs in the AZP
- Overview tab to see summary of assigned subnets, interfaces, and rules, look
##### NSGs and Subnets
- can assign NSG to a subnet and/or create DMZs
- rules here restrict flow to all machines within the subnet
	- Subnets can only have one NSG associated
##### NSGs and Network Interfaces
- can assign directly to the NIC of an Azure resource
- rules here restrict flow to the specific interface only
	- NICs can only have 1 NSG associated

### Determine NSG rules
- Enable the filtering of traffic to/from devices or entire subnets within an NSG
##### Things to know
- There are some default rules created by Azure and applied to ALL NSGs 
- Cannot be removed, can be overridden using priority values
	- DenyAllInbound
		- Deny's all inbound traffic
	- AllowVnetInbound
		- allows traffic from other machines within the same virtual network
	- AllowAzureLoadBalancerInbound
		- allows traffic from your Azure load balancers
	- DenyAllOutbound
		- Denys all outbound traffic
	- AllowInternetOutbound
		- allows outbound to the internet (port 80/443)
	- AllowVnetOutbound
		- Allows traffic outbound to other machines on the virtual network
- Can also add custom rules by specifying conditions for:
	- Name, Priority, Port(s), Protocol (TCP/UDP), Source (any/IP addresses/service tags), Destination (any/IP addresses/service tags), Action (Allow/Deny)
	- Priority values go low to high
		- lower the number, the higher the priority

### Determining NSG effective rules
##### Things to know
- Each NSG is evaluated independently
- Order in which Azure processes each NSG depends on if Outbound or Inbound traffic
- Inbound traffic
	- Subnet NSGs first, then interface NSGs
- Outbound traffic
	- Interface NSGs first, then subnet NSGs
##### View effective rules
- Viewing the NSG in the AZP, use Help > Effective security rules tool
- This shows which rules from the NSG are actually applied to each machine, subnet, or NIC within the NSG

### Create NSG rules
- Can all be taken care of in the AZP
##### Things to Know 
- source
	- controls inbound traffic, allow or deny
	- can be any resource, IP address or range, application security group, or tag
- destination
	- same as source, but for outbound traffic
- Service
	- destination protocol and port or port range
	- Can use a predefined service or a custom port or port range
- Priority
	- order in which rules are processed
	- lower numbers will take precedence
	
### Application Security Groups
- used to group VMs based on workload
- can define NSGs based on these app groups
##### Things to know
- 