Tags: [[365]] [[cloud]] [[entra]] [[identity-management]]
# Secure Your Identities with Entra
### About
###### Author: *Bearded 365 Guy*
###### URL: *https://www.bearded365guy.com/products/secure-manage-microsoft-365-business-premium*
###### Published: *04/01/2026*
-------------------------------------------------------------------
## Notes
### Conditional Access
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
		- Excluded from most policies
		- Should always have at least 2 accounts in this group
			- Not used for anything else
			- very strong password
			- heavily audited
	- Pilot group (testing)
		- CA-PilotUsers
		- small amount of users, preferably different use cases, semi tech-savvy
		- always deploy policies to this group first
	- Contractors group (external) 
		- CA-Contractors
		- useful for users that may have licensed accounts, but not technically employed by the org
		- may have personal devices
- For targeting all users, use the built in in the conditional access policy
- For targeting admins, use the directory roles, rather than groups
Entra > Entra ID > Groups
- Create new group, security group, assigned, admin account as owner
#### Policies
- additive
	- policies stack on top of each other
	- do not need to have the same controls in multiple policies
- create a baseline, then add more controls for specific scenarios
- Roll out one policy at a time
- Sign in logs show all policies applied and controls required
##### Naming Convention
- CAx - \<Targeted Users\> - \<What it's doing\>
	- x is the policy number
	- Targeting Users is who the policy is targeting
	- What the policy is doing....
##### Good Baselines
CA1 - All Users - Block Legacy Authentication
Assignments
- Users or agents
	- Include: All users
	- Exclude: CA-BreakGlass
- Target Resources
	- All resources
- Network
	- n/a
- Conditions
	- Client Apps > Legacy Authentication Clients (Exchange ActiveSync clients, other clients)
Access Controls
- Grant
	- Block access
- Session
	- n/a
CA2 - All Users - Require MFA
Assignments
- Users or agents
	- Include: All users
	- Exclude: CA-BreakGlass
- Target Resources
	- All resources
- Network
	- n/a
- Conditions
	- n/a
Access Controls
- Grant
	- Grant access, require auth strength, "Auth Strength - Baseline" (was created earlier)
- Session
	- n/a
CA3 - BreakGlass - Require Phish Resistant MFA
Assignments
- Users or agents
	- Include: CA-BreakGlassAccounts
- Target Resources
	- All resources
- Network
	- n/a
- Conditions
	- n/a
Access Controls
- Grant
	- Grant access, require auth strength, "Auth Strength - Admin" (was created earlier)
- Session
	- n/a
CA4 - Admins - Require Phish Resistant MFA
Assignments
- Users or agents
	- Include: Directory Roles > Administrative roles
		- 
- Target Resources
	- All resources
- Network
	- n/a
- Conditions
	- n/a
Access Controls
- Grant
	- Grant access, require auth strength, "Auth Strength - Admin" (was created earlier)
- Session
	- n/a

TAP (Temporary access Password)
- If a user loses access to MFA device:
	- do not temporarily disable MFA or remove sign in methods to force re-enrollment
	- use TAP to grant the user access, then have *them* re-register new device
### Guest Access
![[Pasted image 20260408191948.png]]
### Enterprise Applications
- Do not allow users to consent to app registrations, must be reviewed by admin
- Entra ID > Enterprise Apps > User consent Setttings
	- Do not allow user consent
- Entra ID > Enterprise Apps > Admin consent Setttings
	- Users can request admin consent to apps they are unable to consent to
	- Set users to approve requests
	- Keep on email notifications
	- 30 days is fine
- Review apps regularly and remove unneeded ones
### Admin Roles
- Least privilege
- There are many restricted admin roles
	- Password Administrator, Exchange administrator, etc
- GDAP
	- Try to move away from shared global admin accounts, use GDAP instead
	- Do not give all users global admin, give specific roles
- PIM