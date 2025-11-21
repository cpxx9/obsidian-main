Tags: [[networking]] [[network-routing]] [[network-protocols]] [[network-security]]
# Network Segmentation
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42186960#overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
##### Firewalls
- software or hardware based
- virtual or physical
- host-based or network-based
- performs NAT and PAT
###### Packet-Filtering Firewall
- permits or denies traffic based on the packet header
	- uses ACLs (Access Control Lists) to determine whether to permit or deny
	- Access-list 100 deny ip any any
		- blocks any port from any IP into the network
###### Stateful Firewall
- inspect traffic as part of a session
- if a host inside the network creates an outbound connection through the firewall, the firewall will let response traffic back in
- if a new destination tries to start a session from the outside in, it will be denied
- more granular than packet filtering

Combination
- most firewalls now use a combination of both
- ACLs to specifically allow/deny certain traffic, and then use sessions for more security
- access-list allow ip any 443
	- this would normally allow any traffic on 443, even if originating from outside
	- combined with statefulness, will only allow port 443 in, if a host from inside initiated the session
###### NextGen Firewall (NGFW)
- deep packet inspection and filtering
- operate at L5, L6, L7 to get in dept information about the packet
- WAFs (Web Application Firewalls) are NGFWs

Example ACL
access-list 100 permit tcp any 192.168.1.0 0.0.0.255 eq www
access-list 100 permit tcp any 192.168.1.0 0.0.0.255 eq ssh
access-list 100 deny    tcp any 192.168.1.0 0.0.0.255 eq telnet
!
Interface Serial 1/0
	ip access-group 100 in

###### Unified Threat Management (UTM) Device
- combines firewall, router, IDS/IPS, anti-malware, and more into a single device
- physical or virtualized, cloud solutions
##### Access Control List
- list of permissions associated with a network resource
- works top to bottom
- put more specific rules at the top
###### Standard Rules
- Deny incoming traffic from internal, private loopback, and multicast addresses from the internet
- Block incoming requests from protocols that should only be used internally
	- SMB, ICMP, etc.
- block all IPv6 traffic if not using it in your network
	- if using in your network, only allow to authorized hosts/ports

Explicit Allow - Implicit Deny
- deny all traffic unless explicitly allowed
Implicit Allow - Explicit Deny
- allow all traffic unless explicitly denied
##### Segmentation Zones
Trusted Zone
- intranet/LAN
- usually allow most traffic from trusted zone to trusted zone
Untrusted Zone
- internet or other outside networks
- only allow return traffic for a session initiated by the trusted zone inbound
- allow trusted zone to talk outbound to untrusted zone
###### DMZ / Screened Subnet
- semi trusted
- devices that need some restricted access from Untrusted Zones and Trusted zones
	- web servers, email servers, etc.
- allow traffic from the internet over specific service ports even if not requested/initiated
	- allow all port 80/443 traffic from internet to web servers, etc.
	- would not allow SSH, RDP, FTP, etc.
- trusted zone treats the DMZ like other untrusted zones
	- allow return traffic is session initiated from trusted zone
	- deny traffic if initiated from DMZ to the trusted zone
##### Jumpbox
- specific device used to communicate from trusted zone to DMZ
- more hardened than other devices in the trusted zone
- do not allow any device in trusted zone to talk with DMZ besides the jump box
- should have minimum permissions and well protected
##### Content Filtering
- Restricting access to content, websites, applications based on specific criteria
URL Filtering
- blocks access to sites based on the URL
Keywork Filtering
- scan webpage for specific defined keywords, block the page if they are detected
- requires more tuning to configure
Protocol/Port Filtering
- block traffic based on ports
###### Proxy Server
- used as an intermediary between a user device and the internet
- can perform all content filtering for multiple devices
- filter malicious traffic and prevent unauthorized access
- hide IP addresses of client devices
- block content to specific URLs/keywords
- cache frequently accessed resources to increase performance
##### Internet of Things
##### SCADA and ICS
##### Bring Your Own Device
##### Zero-trust Architecture
##### Virtual Private Network (start here)
##### Using VPN Connections
##### Remote Access Management