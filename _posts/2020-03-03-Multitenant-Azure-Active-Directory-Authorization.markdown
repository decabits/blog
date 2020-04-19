---
layout: post
title:  Making an Azure Active Directory Multitenant OAuth Application
date:   2020-03-27 09:57:36 +0530
categories: OAuth Azure Microsoft Active Directory
---

So recently we had do an interesting integration with <a href="https://azure.microsoft.com/en-in/services/active-directory/">Microsoft's Azure Active Directory</a>. The use case was to get access of all the users in microsoft active directory of our clients/businesses.
In this article we will walk through all the steps required to achieve that.

### Step 1 - Register an application on Azure Portal

You need to register an OAuth application in your azure portal.

- So first thing you need to do is to log in/register to [Azure Portal](https://portal.azure.com/).
- Once logged in please open Active Directory (create a new directory if required).
- Now click on **App Registrations** in the left panel as depicted in the screenshot below and create a new application.
- Fill out the details for your application form. Make sure to select **Accounts in any organizational directory** as it is going to be a Multitenant application.

<img src="/assets/images/azure/azure-active-directory.png" alt="Azure Active Directory" style="width:80%; margin:auto;">

New App Sample - 

<img src="/assets/images/azure/azure-new-app.png" alt="Azure Active Directory New App" style="width:80%; margin:auto;">


### Step 2 - Get the access from active directory administrator

Once your app is registered you can access it using a unique URL for your OAuth application which will look like -

```
https://login.microsoftonline.com/da2242ef-5ee5-4315-b939-2d05e11b533a/oauth2/v2.0/authorize?client_id=4b424178-e809-4f8e-9dfa-bd0bc290762b&response_type=code&redirect_uri=https%3A%2F%2Fdecabits.com/azure/callback&response_mode=query&scope=offline_access%20user.read.all%20user.read&state=12345
```

Lets break it out and understand the use of each semantic -

- **https://login.microsoftonline.com/** - Base URL used for login
- **da2242ef-5ee5-4315-b939-2d05e11b533a** - Your active directory specific tenant Id. 
- **client_id=4b424178-e809-4f8e-9dfa-bd0bc290762b** - Your application/client id after registration
- **redirect_uri=https%3A%2F%2Fdecabits.com/azure/callback** - Same redirect uri as you added while app registration
- **scope=offline_access%20user.read.all%20user.read** - The permissions you need from user, most important here is read all users

Now if you are part of tenant with id `da2242ef-5ee5-4315-b939-2d05e11b533a` and you have read access to all users you should be able to login successfully and provide the access code back to the redirect URI that can use it to get authorization/refresh token which will later be used to fetch user information.


The problem with above is that it is allowing access to a single-tenant i.e `da2242ef-5ee5-4315-b939-2d05e11b533a`, so how can we make it multi-tenant i.e general. There are two ways - 

Instead of specific tenant you can use - 

1. **common** - Allows any microsoft user to login but only gives personal access so read all users will not be granted, so not correct for our use case.
2. **organizations** - Allows only organization accounts to login and can give access to read all user if logged in user is user/global adminstrator.

So we replace the specific tenant with a multi-tenant allowing value i.e `organizations`. Our new url is -

```
https://login.microsoftonline.com/organizations/oauth2/v2.0/authorize?client_id=4b424178-e809-4f8e-9dfa-bd0bc290762b&response_type=code&redirect_uri=https%3A%2F%2Fdecabits.com/azure/callback&response_mode=query&scope=offline_access%20user.read.all%20user.read&state=12345
```

Once you open the link, it should look like - 

<img src="/assets/images/azure/azure-ad-login-link.png" alt="Azure Active Directory New App" style="width:80%; margin:auto;">


### Step 3 - Exchange code for authorization token & refresh token and fetch all users

If you reached so far, you are done with the main part, now all that is left is to fetch the authorization token and fetch the users.

I will really recommend to follow official microsoft documents from hereon to make sure you make the correct API call -   

1. Get authorization token - [Here](https://docs.microsoft.com/en-us/graph/auth-v2-user#3-get-a-token)
1. Refreshing token - [Here](https://docs.microsoft.com/en-us/graph/auth-v2-user#5-use-the-refresh-token-to-get-a-new-access-token)
1. Accessing API - [Here](https://docs.microsoft.com/en-us/graph/auth-v2-user#4-use-the-access-token-to-call-microsoft-graph). Make sure to replace `GET https://graph.microsoft.com/v1.0/me` with `GET https://graph.microsoft.com/v1.0/users` to fetch all users.

Vola!! You have integrated users from your clients/business into your platform.

<strong>If you face any issues, please feel to reach us at info@decabits.com. We'll be happy to help you out. Cheers!!</strong>
