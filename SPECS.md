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

# Estimations

## Setup Azure B2C tenant and all required policy and custom domains
- 1 day

## User sign up flow story
- we can customize sign up flow for one or more apps. For example, the default sign up will be asking for 
  - email, firstname, lastname
  - but then we can create a different sign up screen for a more secure app which ask for mobile number as well
  - the sign up screen can be customized using pure html and JS and CSS
  - Estimation for 1 sign up flow: 
    - 1 day for simple, 
    - up to 5 days for more complex screen (e.g. adding ReCaptcha, or to send SMS verification during sign up process or external API integration (claim exchange))

## Multifactor Authentication
- Standard MFA using Authenticator app:
  - Enable/Disable or Enforced per user AND per policy (this is a settings in Azure Portal)
    - if we enable MFA on a user then next time when user login, they will be asked to setup MFA using their mobile or Authenticator app or phone call !!!
    - note: you can customize the MFA setup screen (need to investigate)
  - Estimation: 
    - configuration in Portal
    - if you want to customize the MFA screen: 1d for simple, upto 5 days for complex customization
- Adaptive MFA:
  - in Azure B2C you can configure condition when MFA is required (e.g. device platform, location, custom filter using expression)
    - configuration in Portal 

## Password self service management (via email)
- we can create 1 single Password self service flow for the whole tenant, where user is asked to enter the email address
- we can customize the "Forgot my password" form
- Estimation: 
  - 1h for using the out of the box (very basic styling change)
  - 1d for simple customization
  - 1d+ for complex

## password policy (no expiry, only complexity)
- this is set per flow (best practice is to make sure the same password policy is used in all flows)
- note: a flow is used to provide "different" login experience (or custom claims) for different apps
- Estimation:
  - configuration in Portal

  
## email verification flow
- if user sign up with email and password, in Azure B2C it is `REQUIRED` to verify the email (you can't sign up until the email is verified)
- The email that is sent to user is `NOT` customizable out of the box for Azure B2C (the subject is "Microsoft on behalf of XXX"). To customize this email, you will need to use Sendgrid
- Estimation:
  - out of the box (no customization)
  - 1d for customizing email using Sendgrid (assuming Sendgrid account is already setup)


## user can change user profile (self service) in B2C
- in Azure B2C , you can capture several user attributes: firstname, lastname, address, job title,etc AND custom attributes (e.g. Department Name) 
- when user signup, they are asked to fill in those details (you can configure which properties are required/not required)
- you can configure which properties are returned in the JWT
- if you turn this on AFTER user has sign up, next time when they login, they are asked to fill in those details
- if you want user to update their profile, then you have to provide them with a link to the profile update link in Azure B2C
- Estimation:
  - out of the box (no customization)
  - 1d for profile update screen (simple) 
  - 5d for complex update screen 

## 3rd party integrator: create new Client Credential app in Azure B2C only
- you can login to Azure portal and create new client (only Admin of the B2C Tenant can do this)
- if you want to create new client via API, you can do this using graph API
- Estimation:
  - out of the box (no customization)
  - via Graph API: this need to be built in your client app

## external Authentication provider: Google, Facebook, Microsoft
- you can configure Azure B2C to use Identities from any other OIDC provider (including another Azure B2C tenant)
- built in are:
  - Google, Facebook, Microsoft (complete list: https://docs.microsoft.com/en-us/azure/active-directory-b2c/add-identity-provider)
- Estimation:
  - out of the box (no customization required)
    
## Single Sign Out
- you configure the front channel logout per Client (Azure B2C does not support Back channel logout)
- Azure B2C will make request to those endpoints when user click on Sign Out (using IFrames)
- each client apps will need to acknowledge the request from Azure B2C and kill user session (on the Client app)
- Estimation:
  - out of the box (no customization required)

## B2C Pricing estimation
- Tiers:
  - P1 tier: free for the FIRST 50k Montly Active Users (meaning only the users that login at least once in that month)
    - you pay 0.0044 AUD per additional MAU (e.g. $220 for 100,000 users)
  - P2 tier: free for the FIRST 50k Montly Active Users (meaning only the users that login at least once in that month)
    - you pay 0.022 AUD per additional MAU (e.g. $1,100 for 100,000 users)
    - 

## Total estimate
- Setup Tenant: 1d
- User Sigup flow: 2-5 day
- MFA setup: 1-5 day
- password self management: 1h - 1d
- password policy: 1h
- email verification: 1h - 1d
- profile update: 1-5 day
- 3rd party integrator: 1h
- External authentication: 1h
- Sign sign out:1h
- Total: 
  - Min: 6 days (simple out of the box style changes only)
  - Max: 19 days (high complex customization)



