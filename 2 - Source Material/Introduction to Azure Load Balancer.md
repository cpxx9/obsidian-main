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
- 