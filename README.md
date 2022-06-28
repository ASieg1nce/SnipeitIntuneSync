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
It also checking if the models, categories and manufactures already existing in Snipe-it. If not, its create it.
Its updating existing Assets in Snipe-it, if a changed was made in Intune
and of cause its create a new Asset in Snipe-ie, if the Asset does not exist.

Its not creating any user, in our instance users are created automatically via. LDAP

# Where does it works

The script is running in Azure Service 'Automation',
so it automatically runs every day and sync all Assets.
