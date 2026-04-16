Tags: [[365]] [[cloud]] [[entra]] [[identity-management]]
# Get Devices Managed with Intune
### About
###### Author: *Bearded 365 Guy*
###### URL: *https://www.bearded365guy.com/products/secure-manage-microsoft-365-business-premium*
###### Published: *04/01/2026*
-------------------------------------------------------------------
## Notes
- control and visibility into devices
- access decisions can be based on devices
- not here to judge how people work
	- here to understand, and build something that is secure and works for *them*
### Device Ownership and Trust Models
##### Corporate Owned
- Highest trust
- Patched regularly, encrypted, joined and company policies applied
- IT fully manages, 
##### BYOD
- Medium trust
- May not be patched, encrypted, etc. 
	- up to each user
- IT manages the company apps, data, etc. 
	- no access to personal data
##### Unmanaged
### Join Types
- How a device is joined to Entra ID / Intune
	- determines what Intune can do with the device
##### Entra Joined
- Registered directly with and only with Entra ID
- cloud native
- no on-prem AD join
##### Hybrid Entra Joined
- Joined to an on-prem AD server
- Also registered in Entra
##### Entra Registered
- Personal BYOD devices
- Shows up in Entra/Intune, but not fully managed
- App level controls available
	- no device level controls

## Enrollment
#### Restrictions
- Create restriction profiles to stop personal devices, set OS version requirements, etc.
#### Autopilot
- designed for Company devices ONLY
- User just signs into device with work credentials
- Security Settings, Compliance Policies, Configuration Profiles from Intune are automatically applied
- Applications automatically installed
##### v1 
- Classic, user driven Autopilot
- Built around hardware registration
- Device is claimed by tenant, before the user receives it and signs in
- more control, more enforcement before deployment
- Good for hybrid-join environment
- More complex to set up
###### Setup
- Relies on hardware IDs to get devices into Intune
- Options to get IDs into Intune
	- Work directly with Hardware vendor
		- they can get the hardware hashed into Intune at time of purchase, before the device is even shipped
		- gold standard
	- Powershell
		- Can run script to get hardware ID
##### v2
- Autopilot Device Preparation
- Good for cloud only environments
- more post-enrollment configuration enforcement
- More heavily relies on Conditional Access and Intune configuration profiles being set up correctly
###### Setup