Tags: [[networking]] [[network-protocols]]

# Ports and Protocols
### About
###### Author: *Jason Dion*
###### URL: *https://udemy.com/course/comptia-network-009/learn/lecture/42185608#overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
##### ICMP
- Used for error reporting and testing
	- when service/host is unreachable
		- ping command
	- when a packets TTL (time to live) has expired
	- when a router cannot forward packets because buffer is filled up

##### Email
SMTP
- port 25
- outbound email, only emails sent
- SMTPS
	- port 465 or 587
	- secure version of SMTP
	- uses TLS or SSL to create secure tunnel and then use SMTP to send traffic over that tunnel
POP3
- port 110
- inbound email, used to receive emails from remote server to a client device
- older protocol, does not allow for easy use on multiple devices
	- messages can only be received from server on one client device, then they are deleted from server
	- newer versions kept a copy on server, so messages can be received by multiple devices
		- read status, delete status, organization (folders, etc.) does NOT work on multiple devices
- POP3S
	- port 995
	- secure version of POP3
	- uses TLS or SSL to create secure tunnel and then use POP3 to send traffic over that tunnel
IMAP
- port 143
- inbound email, allows for read status, deletion, organization to all be synced across devices
	- client devices manage emails on the server itself, does not download email from server
- IMAPS
	- port  993
	- secure version of IMAP
	- uses TLS or SSL to create secure tunnel and then use IMAP to send traffic over that tunnel

##### File Transfers
FTP (File Transfer Protocol)
- ports 20 and 21
- 20
	- the actual data transfer
- 21
	- sending control command
- not encrypted
SFTP (Secure/SSH File Transfer Protocol)
- port 22
- Tunnels an FTP protocol through an SSH tunnel, which is encrypted
TFTP (Trivial File Transfer Protocol)
- port 69
- no user authentication, directory browser, etc.
- for sending files when minimal security is needed
SMB (Server Message Block Protocol)
- port 445
- allows computer applications to read and write to files and request services from server programs
- Windows file sharing
- SAMBA
	- Cross-platform version that works on systems like Linux
- used inside LANs
	- not used to send files over the Internet

##### Remote Access
SSH
- port 22
- provides secure channel over an insecure network in client-server architecture
	- secures remote login and other services over an insecure network
- Strong authentication and data encryption
- used to operate text-based commands
Telnet
- port 23
- used for operating text-based commands in LANs
- Not secure, sends data in plain-text
- not really used, use SSH if the equipment supports it
RDP
- port 3389
- proprietary protocol to allow GUI to Windows systems over remote connection
- Encryption, smart card authentication, bandwidth reduction methods, etc.

##### Network Services
DNS
- port 53
- translates domain names into IP addresses
- uses TCP and UDP
DHCP
- port 67/68
- automates assignments of network configurations
- servers listen on 67, clients receive over 68
SQL Services
- port 1433 (Microsoft SQL) / 3306 (MySQL)
- for authentication and database management by users
SNMP
- port 161/162
- collecting info from and configuring network devices
	- servers, switches, UPS, etc.
- port 161 used by SNMP managers for polling
- port 162 used by client devices to send info to SNMP server (trap messages)
Syslog
- port 514
- used to send event message logs to server known as collector
- uses UDP (default) or TCP (if reliability is needed)
NTP (Network Time Protocol)
- port 123 UDP
- used to synchronize clocks of devices over a network
SIP (Session Initiation Protocol)
- port 5060 TCP and UDP 
	- unencrypted
- port 5061 TCP for encrypted
- used for initiating, maintaining, and terminating real time communication services
	- VOIP, video streaming
LDAP (Lightweight Directory Access Protocol)
- port 389 TCP and UDP
- used to access and maintain distributed directory information over a network
- LDAPS
	- port 636
	- over SSL/TLS tunnel
