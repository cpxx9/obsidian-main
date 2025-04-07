Tags: [[azure]] [[azure-networking]] [[networking]] [[az-104]] [[cloud]] [[network-routing]] [[high-availability]]

# Introduction to Azure Load Balancer
### About
###### Author: *MSoft*
###### URL: *https://learn.microsoft.com/en-us/training/modules/intro-to-azure-load-balancer*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
- Distributes traffic across a set of VMs in a pool
- VMs in pool can be Azure IaaS VMs, instances in a VM Scale Set, etc.
- configurable with rules
- Health probes ensure traffic is not sent to "down" VMs in the pool
### What is Azure Load Balancer
- When incoming traffic becomes too much for one server to handle, you can 
	- continuously add more resources to the one server, vertical scaling
	- add more servers behind a load balancer, horizontal scaling
- usually more lower end servers work better than one higher end server
- load balancers ensure smooth operation between multiple servers
- rules determine how traffic is distributed to VMs in the pool
- health probes ensure that traffic is not sent to unhealthy VMs in the pool
- Can be public or private
	- Public, balance internet traffic to VMs
		- maps public IP and port of the incoming request t private IP and port of the pool VMs
		- ex. distribute load of incoming web requests from internet across multiple servers
	- Private, distributes traffic internally
		- never directly exposed to the internet
		- examples
			- internal business apps that run in azure and can only be accessed from Azure or on-prem resources
			- balance traffic from front-end web servers to secondary back end VMs for data processing
		- internal load balancers used for
			- within a vNet
				- VMs in the vNet to another set of VMs in the same vNet
			- hybrid environments
				- on-prem computers to set of VMs in vNet
			- multi-tiered applications
				- internet facing applications with a backend tier not exposed to the internet
			- LOB applications
				- fully internal applications that are not accessible to internet
- Can be used for inbound or outbound traffic flow
- Can scale up to millions of TCP and UDP application flows
### How Azure Load Balancer Works
- Operates at Transport layer (layer 4) of OSI model
	- allows traffic management based on, source and destination address, protocol type (TCP/UDP) and port number
- Several elements work together to ensure high availability
	- front end IP, load balancer rules, backend-pool of VMs, health probes, inbound NAT rules, high availability ports, outbound rules
#### Front-end IP
- address that clients use to connect to the load balanced application
- can be public or private
- can have multiple IPs
#### Load balancer rules
- defines how traffic is distributed to the pool
- maps front-end IP and Port (source) to backend IP and port (destination)
- traffic managed with 5-tuple hash made of
	- Source IP, IP of the requestor
	- Source Port, port of the requestor
	- Destination IP, IP of the requested service
	- Destination Port, port of the requested service
	- Protocol type, UDP or TCP
	- Session affinity, ensures that the the same back-end VM handles all traffic for a specific client
- can balance services on multiple ports, IPs or both
- Layer 4 operations only, if layer 7 is needed, something like Azure Application Gateway is needed
#### Back-end pool
- groups of VMs or instances in a VM Scale Set 
- respond to incoming requests 
- usually cheaper to add more instances to back end pool than to scale vertically
- as new instances are added to the pool, Azure handles reconfiguring everything based on rules you already have in place
#### Health probes
- determines the health status of instances in the back end pool
	- Load balancer sends traffic or not based on this determination
- Can define thresholds for healthy vs unhealthy
- Load balancer stops sending new connections if unhealthy
	- old connections are not affected or stopped unless
		- application ends the flow
		- idle timeout occurs
		- VM shuts down completely
#### Session persistence
- load balancer distributes network traffic equally among all instances in the pool by default
	- stickiness is only provided within the same transport session
- Session persistence describes how traffic from a client should be handled
	- default is that any health instance in the pool can accept successive requests from a client
- uses hash made up of source and destination IP (sometimes protocol as well) to route traffic to back-end pool instances
	- can choose between
	- none (default), any healthy VM can accept subsequent requests
	- Client IP (2-tuple hash), the same back-end instance must handle subsequent requests from the same client IP, regardless of protocol
	- Client IP and protocol (3-tuple hash),  the same back-end instance must handle subsequent request from the same client IP and protocol
#### High availability ports
- load balancer rule such as `protocol - all and port - 0` is called High availability (HA)
- enables a single rule to load balance all TCP and UDP flows that arrive on any port of an *internal* load balancer
#### Inbound NAT rules
- can combine load balancing rules and NAT rules
- example, can use NAT from load balancer's public IP address to TCP 3389 on a specific VM, allowing RDP access
#### Outbound rules
- configures SNAT for all VMs in the backend pool
- enables instances to talk outbound to the internet or other public endpoints

### When to use Azure Load Balancer
- applications that need high performance and ultra low latency
- if you already have on prem load balancers that need to be replaced
- balance traffic for front end tier of web apps
	- internal load balancers for communication between front end and back end tiers
- Can use inbound NAT rules to enable RDP
#### When not to use Azure Load Balancer
- web applications with small amounts of traffic
- applications that need a WAF (Web Application Firewall)
- other load balancing services available in Azure that may be better suited for some needs
	- Azure Front Door
		- application delivery network, global load balancing and site acceleration
		- offers layer 7 capabilities like TLS/SSL offload, path-based routing, fast failover, a web application firewall, and caching to improve performance and high availability of your applications
		- Good for web app deployed across multiple regions
	- Azure Traffic Manager
		- DNS based load balancer, not as fast at failover