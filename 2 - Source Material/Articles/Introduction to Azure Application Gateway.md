Tags: [[azure]] [[azure-networking]] [[networking]] [[az-104]] [[cloud]] [[network-routing]] [[high-availability]]

# Introduction to Azure Application Gateway
### About
###### Author: *MSoft*
###### URL: *https://learn.microsoft.com/en-us/training/modules/intro-to-azure-application-gateway/*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
- Azure service for processing traffic to web apps
- Load balances http(s) traffic
- inspects traffic with WAF
- encrypts traffic
### What is Azure Application Gateway
- manages client requests to web apps hosted in a back end pool
	- Azure VMs, VM Scale Sets, Azure App Service, or on-prem servers
- Load balances http(s) traffic, inspects traffic with WAF, encrypts traffic
- round-robin process
- session stickiness, keeping clients routed to the same back end server
	- good for transactions, etc.
- Support for HTTP(S), HTTP/2, and WebSockets
- Supports auto scaling, dynamically adjusts capacity
- Allows graceful removal of back end pool servers for maintenance
	- connection draining, stops new connections and slowly gets rid of existing ones

### How Azure Application Gateway Works
- series of components that work together
- Front-end IP address, can be public, private, or both (one of each max)
- Listeners, one or more receive incoming requests, route to back end pool based on rules that you set up, handles TLS/SSL certs. Can be basic or multi-site
	- basic can only route based on the path
	- multi-site can also route based on the hostname 
- Routing rules, bind listeners to back end pool, specifies how to traffic based on the url of a request, indicate whether and how traffic is encrypted
	- how you configure session stickiness, connection draining, RTO period, etc.
#### Load balancing in Application Gateway
- automatically load balances with a round robin method
- routes traffic based on routing parameters
- can configure so that all requests for a client in the same session are routed to the same server
#### Web application firewall (WAF)
- optional component
- handles requests before getting to a listener
- checks request for common threats as defined by OWASP (Online Web Application Security Project)
- OWASP defines rule sets, 3.1 is the default if WAF is turned on
	- can apt to only check for specific rules in a set
	- can customize which parts of a request are examined, limit size of uploads
#### Back end pools
- collection of servers, can be VMs, scale set, Azure App services App, or on prem servers
- each pool has its own load balancer
- if using Azure App services for back end pool servers, encryption works out of the box
	- certificates need to be manually set up if not
#### Application Gateway routing
- can be path based or multi-site
##### Path Based Routing
- routes different paths to different servers
	- /video/* to one pool, /images/* to another pool
##### Multi-site routing
- sends traffic to a back end pool based on the fqdn
	- contoso.com to one back end pool, test.com to another one
