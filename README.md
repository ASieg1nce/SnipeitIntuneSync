# SnipeitIntuneSync
This Powershell script Sync Intune Assets to a Snipe-it Instance.

Used Modules are:
- SnipeitPS
- Microsoft.Graph.Intune

# How does is works

The Script extract at first all Assets / Entries from Intune and searching for double serial numbers.
If it find multiple serial numbers it just use the Entry with the latest enrollment date.
All other Entries with double serial numbers ignored.

After this its compare all Intune Assets with Assets in Snipe-it.
It also checking if the models, categories and manufactures already existing in Snipe-it. 
If these do not exist the script create models, categories and manufactures.

If the Asset does not exist in Snipe-it the script create a new Asset,
its also updating the assets in Snipe-it iff a changed was made in Intune.

Its not creating any user.
But you can sync users automatically via. LDAP sync in Snipe-it.

# Where does it works

The script can run locally or in Azure Service 'Automation'.


*Best practice: I recommended to make a backup of Snipe-it before trying the script for the first time.
