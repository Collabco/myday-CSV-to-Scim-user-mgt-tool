# myday-CSV-to-Scim-user-mgt-tool
Command line tool for import of users, groups and memberships to myday

This repository will host the binaries of this tool, and is licensed for use by customers of Ready Education with their myday tenancies. 

No license is given to use, copy, redistrubute this software commercially or for free by any other parties.


# CSV to SCIM command line tool

usage:
csvtoscim -csv <file.csv> -mappings <mappings.json> -tenant <tenant ID> -clientId <SCIM client ID> -secret <SCIM client secret> -action <action to perform>

In order to use this tool, you must have a valid client set up in your myday tenancy. Follow this guide to create a new client, using the SCIM.FULL_ACCESS scope.
https://collabco.elevio.help/en/articles/106

NOTE, DO NOT USE THE CLIENT SET UP FOR AAD SYNC. IT WILL GENERATE TOKENS WITH A 3 YEAR EXPIRY ON EACH REQUEST WHICH WILL BE STORED FOR THAT PERIOD AS A NEW TOKEN WILL BE GENERATED ON EACH RUN OF THE TOOL. PLEASE CREATE A NEW CLIENT SPECIFICALLY FOR USE WITH THIS TOOL WHICH WILL HAVE THE TOKEN EXPIRY SET TO 1 HOUR AUTOMATICALLY.
  

- CSV file must have headers to be able to map which columns in the CSV are mapped to the SCIM entity being imported (user, group or membership)
- mappings file must be a json format document that follows the following format
{
  Entity: "User/Group/Membership"
  MapRules: [
	{
		"IncomingColumnName": "csv column name",
		"OutGoingColumnName": "SCIM field name"
	},...
  ]
}

actions available:
- addUsers
- addGroups
- removeUsers
- removeGroups
- addMemberships
- removeMemberships
- updatePasswords
