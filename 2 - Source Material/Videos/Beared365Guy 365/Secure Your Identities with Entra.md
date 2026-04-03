Tags: [[365]] [[cloud]] [[entra]] [[identity-management]]
# Secure Your Identities with Entra
### About
###### Author: *Bearded 365 Guy*
###### URL: *https://www.bearded365guy.com/products/secure-manage-microsoft-365-business-premium*
###### Published: *04/01/2026*
-------------------------------------------------------------------
## Notes
#### MFA Strategy and Authentication Strengths
- Admins must have stronger authentication requirements
Entra > Entra ID > Authentication Methods
- Disallow methods that are no longer strong
	- SMS, phone call, email
- Enable newer methods
	- Passkey (FIDO2)
Entra > Entra ID > Conditional Access > Authentication Strengths
- create auth methods for different levels of user (admin, standard, etc.)
- Admin should only allow the strongest methods
#### Identity Groups
-  Consistent group naming convention
	- DOCUMENT!!
	- Break Glass group(emergency use only)
		- CA-BreakGlassAccounts
	- Pilot group (testing)
		- CA-PilotUsers
	- Contractors group (external) 
		- CA-Contractors
- For targeting all users, use the built in in the conditional access policy
- For targeting admins, use the directory roles, rather than groups
Entra > Entra ID > Groups
- Create new group, security group, assigned, admin account as owner