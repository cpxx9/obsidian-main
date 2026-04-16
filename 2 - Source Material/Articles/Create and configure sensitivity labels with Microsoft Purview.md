Tags: [[365]] [[cloud]] [[entra]] [[purview]] [[identity-management]] [[information-protection]]
# Create and configure sensitivity labels with Microsoft Purview
### About
###### Author: *MSoft*
###### URL: *https://learn.microsoft.com/en-us/training/modules/m365-compliance-information-protect-information/information-protection-overview*
###### Published: *n/a*
-------------------------------------------------------------------
## Notes
### Overview
Editing or deleting a sensitivity label
- If deleted, the label isn't automatically removed from content 
- All protection settings continue to be enforced on content that had the deleted label applied
- If edited, the version of the label that was applied to content is what's enforced on that content
#### Elements
- **Label scopes** define the relevance of labels, controlling which settings are visible and how they appear across different applications and services.
- **Label priority** determines the order in which labels are assigned, affecting how they're automatically applied and how they inherit label properties.
- **Sublabels** or grouped labels, improve label management by enabling more detailed classification within broader sensitivity categories.
#### Options
Publish to users and group
- sensitivity labels are assigned to specific users or groups.
Default label for content
- Policies can set default labels for content (documents, emails, meeting invites) and new containers  (Teams, SharePoint sites)
Require justification for label changes
- Policies can require users to give a reason when changing a label, especially if it lowers the data's sensitivity level.
Mandatory labeling for certain content
- Some types of content might need to have a label before actions like saving, sending, or sharing are allowed.
Help links for users
- Policies can include customized help links for more guidance on label use.
Policy priority (order matters)
- The order of label policies shows their priority, affecting how settings are applied in cases of conflict.
Policy application time
- It might take up to 24 hours for changes in label policies to fully apply across an organization.