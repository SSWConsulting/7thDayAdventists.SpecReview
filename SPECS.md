Note: Luke is the PO
MyAdventis: .NET mvc 5 with WCF service with AngularJS (small) . no need to keep the current UI

# do we need a centralized IAM
- less than 5 apps (all web apps)
- do Android and IOS
- 1 desktop app
- how many end users: less than 20k users, long term can go to 40K users

# Auth features
- User sign up
- 2Fa: using SMS code AND Google Authenticator
- password self service management (via email)
- password policy (no expiry, only complexity)
- email verification flow, if user sign up using email and password
- user can change user profile (self service) in B2C
- 3rd party integrator: create new Client Credential app in Azure B2C only
- external Authentication provider: Google, Facebook, Microsoft
- Single Sign Out
- pricing estimation
- how much paying Auth0? 45,000 a year

# Apps 
- MVC (.net framework)
- Angular
- React Native
- .NET Core

# when we migrate, we don't want to migrate the password
- with Azure B2C we need to migrate the user password (1 week)

# Claims
- no additional claims required
- we only use this for Authentication, not Authorization
- we need to return the AventisId

# deadlines?
- 







