# PymecastAutoAdd
A python3 script that allows you to quickly add a single email address to a Mimecast Profile Group.

## Setup/Use
Setup involves creating a Mimecast API 2.0 application in your Mimecast console before running script. Follow instructions below:
  1. Add an API 2.0 application in Mimecast by going to Services -> API and Platform Integrations -> select "Generate Keys" for Mimecast API 2.0
  2. Create app and save the Client ID and Client Secret in a secure location (such as a credential manager)
  3. Obtain the Mimecast Profile Group ID of the group you want to make additions for, and add it to line 32 of this script (You can use the Find-Groups API endpoint for this: https://developer.services.mimecast.com/docs/userandgroupmanagement/1/routes/api/directory/find-groups/post)
  4. Run script, copy/paste Client ID/Secret to generate an access token, and then provide the email and a note for the addition
  5. Press CTRL+C when finished

