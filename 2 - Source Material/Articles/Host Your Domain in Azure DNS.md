Tags: [[azure]] [[az-104]] [[networking]] [[azure-networking]] [[dns]]

# Host Your Domain in Azure DNS
### About
###### Author: *MSoft*
###### URL: *https://learn.microsoft.com/en-us/training/modules/host-domain-azure-dns/*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
Provides a way to manage your DNS records in Azure, helping to keep everything in the same place.
Use the same credentials, APIs, tools, and billing as other Azure resources.
### What is Azure DNS?
- DNS service hosted on Azure infrastructure
- globally distributed name servers
- manage domain servers using existing Azure account
- cannot register through Azure, but acts as the SOA for a domain registered elsewhere
#### What is DNS?
- Translates human readable domain names into IP addresses
	- i.e. google.com to 8.8.8.8 
- Operates using a directory hosted on servers all over the world
#### How does DNS work?
- maintains a portion of the global database of key-value pairs for domain names to IP addresses
	- has authority over a set of domain names
- maintains a local cache of recently used domain names and their IP addresses
	- provides quick response for local domain lookups
- if the server cannot match domain to an IP, it passes request to another DNS server
	- repeats until a match to an IP address is found, or it times out
#### DNS server assignment
- network devices need to be assigned a DNS server to use
- can have a DNS server on premises
- ISPs usually provide one to use automatically
#### Domain lookup requests
- request comes in to DNS server
- checks the local cache, if found it resolves very quickly
- if not found in local cache, reaches out to other DNS servers to find a match
- if a match is found, this server will update it's local cache and resolve the request
	- time depends on how many DNS servers it has to check before finding a match
- if no match is found after some time, the request will error out
#### IPv4 and IPv6
- every network attached device has an IP address
- 2 standards, v4 and v6
- v4
	- 4 binary octets(0-255 in decimal), separated by decimal
	- 127.0.2.1
- v6
	- 8 groups of hexadecimal numbers
	- fe80:11a1:ac15:e9gf:e884:edb0:ddee:fea3
#### DNS settings for your domain
- needs to be configured for each type of host you may have
	- email, web, etc.
#### DNS record types
- DNS config info is stored as files within a zone on the DNS server
	- each file is called a "record"
- different record types for different needs
- A
	- host record, maps domain to IP address
	- google to 8.8.8.8
- CNAME
	- alias record, maps one domain to another
	- www.google.com to google.com
- MX
	- maps mail requests to mail server
	- email to anything @google.com to the google mail server
- TXT
	- maps domain to a text string
	- used to verify ownership, among other things
- Various other types that aren't as common
	- wildcards, CAA (cert auth), NS (name server), SOA (start of auth), SPF (sender policy framework), SRV (server locations)
#### Record sets
- multiples resources defines in a single record
	- if a domain has 2 ip addresses
#### Why use Azure DNS?
- built on the resource manager server, so you get all those benefits
	- improved security
	- ease of use through portal, API, etc.
	- Private DNS domains
	- Alias record sets
- Does not support DNS System Security Extensions
	- Will need to host those portions of DNS in your main provider, or another 3rd party
##### Security Features
- RBAC
	- fine grain control over access to DNS resources, monitor usage
- Activity logs
	- track changes, pinpoint fault
- Resource locking
	- restriction of resource groups, subscriptions, or specific resources
##### Ease of use
- Manage DNS of Azure resources and external resources in the same place
- Same credentials support contract, and billing
- RBAC tied in 
- Can manage through Azure Portal, Powershell, Azure CLI, REST API, SDKs
##### Private domains
-  name resolution for VMs within and between vNetworks
- use your own custom domain names for resources
- no need for a custom DNS solution
- all record types are supported
- hostnames are auto maintained
- split-horizon DNS
	- same domain name in public and private DNS zones
	- resolves based on the originating request locations
##### Alias record sets
- can point to Azure resources
	- public IP address, Azure Traffic Manager profile, or Azure CDN
- can be used for A, AAAA, and CNAME records

### Dynamically resolve resource name by using alias record
- can use load balancers to distribute traffic to 2 or more identical servers
- Easy to set up in Azure
#### What is an Apex domain
- highest level of a domain
- also called zone apex or root apex 
- usually represented by @ in DNS records
- not able to create CNAME records at the apex level
- Azure has alias records that are supported at the apex level
#### What are Azure alias records
- enable apex domain records to reference other Azure resources
	- Traffic Manager Profiles
	- Azure CDN endpoints
	- Public IP resource
	- Front-door profiles
- helps maintain DNS, as it is linked to a resource rather than a specific IP
	- if the resource changes, DNS auto updates
- allow for load balancing 
- supports A, AAAA, and CNAME records
#### Use for Alias records
- ensures records are up to date, as DNS records are tightly couples to the Azure resource
	- if the IP, for example, changes on an Azure resource, the DNS records knows and is updated
- can route to Traffic Manager profiles for load balancing
- can route to CDN endpoints