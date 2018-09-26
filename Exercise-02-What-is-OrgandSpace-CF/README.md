- - - -
Previous Exercise: [Exercise 01 Setup](../Exercise-01-Setup) Next Exercise: [Exercise 3 - Publish Wishlist](../Exercise-03-Publish-Wishlist)

[Back to the Overview](../README.md)
- - - -

Basic Understanding of Org and Space.

Intro: 
On SAP Cloud Platform - Cloud Foundry you will hear terms like Global account, Organization, Spaces, api endpoint. In this document we will explain those terms: 


1.	When you login to SAP Cloud Platform cockpit, you will see the home page which has Global Accounts. 

![screnshot alt text](images/globalaccts.jpg).

Global Accounts: Global accounts are hosted environments that represent the scope of the functionality and the level of support based on a customer or partner’s entitlement to platform resources and services. 
A global account can contain one or more subaccounts in which you deploy applications, use services, and manage your subscriptions. More on [help guide](https://help.sap.com/viewer/e275296cbb1e4d5886fa38a2a2c78c06/Cloud/en-US/c165d95ee700407eb181770901caec94.html?q=global%20accounts) 


2.	On the left side you will see the regions on which SAP Cloud Platform is available, Services that can be used and different notifications.  

![screnshot alt text](images/lefttab.jpg).

3.	Click on the tile with TechEd2018. 

![screnshot alt text](images/tilewithteched.jpg).
4.	Here you will see the two subaccounts. OPP363 and OPP363CF.  
![screnshot alt text](images/subacct.jpg).

Subaccounts: Is the place where you can deploy applications, use services, and manage subscriptions on SAP Cloud Platform.

5.	On left you can see the Entitlements and Members to your Global account.

![screnshot alt text](images/entitlementsmemeber.jpg).

6.	Click on Entitlements to see the quota available to the Global account and to which subaccount it is assigned. 

![screnshot alt text](images/clcikentitlement.jpg).

![screnshot alt text](images/autoscalingentitlement.jpg).

7.	Click on Subaccounts to go back.

![screnshot alt text](images/cforg.jpg).

8.	Click on OPP363CF to go the Organization overview page aka subaccount overview page 

![screnshot alt text](images/orgdetail.jpg).

Organization: An org is a development account that an individual or multiple collaborator can own and use. It has a resource quota plan, applications, services availability, and custom domains.  

9.	On left you can see the Spaces, create Destinations under Connectivity, create Roles and Trust configuration s under Security, view quota assigned to your space, and the Members. 

![screnshot alt text](images/securityandquota.jpg).

Spaces: A space provides users with access to a shared location for application development, deployment, and maintenance.  More information on our [help guide](https://help.sap.com/viewer/e275296cbb1e4d5886fa38a2a2c78c06/Cloud/en-US/8426b2c65ebe4b1fa3ad9e1e571a2f28.html) 

10.	On right you can see the API endpoint and subaccount details. 


![screnshot alt text](images/subacctdetail.jpg).


API Endpoint: The API endpoint, or target URL, for your Cloud Foundry instance is the URL of the Cloud Controller. More information on our [help guide](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/350356d1dc314d3199dca15bd2ab9b0e.html)

11.	Click on Spaces. 

![screnshot alt text](images/spaces.jpg).


12.	Here you can see the space and the related information like started and stopped applications quota assigned.
![screnshot alt text](images/checkquota.jpg).

Make sure you have the available resources as highlighted below. 

13.	Click on the space.  


![screnshot alt text](images/clcikspace.jpg).

14.	This is the overview page of the space, and the operations that you can perform with the resources available to your space. 

![screnshot alt text](images/resourcesoverview.jpg).

15.	On left you can see Services where you can create service instance for your application to use, Routes where you can see the host names, Events and the Member List, Security Groups. 

![screnshot alt text](images/securitygroups.jpg).

16.	Click on Service, to expand it. 
![screnshot alt text](images/clcickservices.jpg).
17.	Click on Service Marketplace. This shows you all the services available to your space which your applications can use 

![screnshot alt text](images/servicemarketplace.jpg).
18.	Click on Service Instances. This is the place where you will be able to see the instances of the services that you have created, and the applications are using it. 
![screnshot alt text](images/serviceinstance.jpg).

User provided Service: User-provided service instances enable you to use services that are not available in the marketplace with your applications running in the Cloud Foundry environment. More information on our [help guide](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/a44355e200b44b968d98ddaa42f07c3a.html?q=User-Provided%20Services) 

19.	This is your Home page. 
![screnshot alt text](images/home.jpg).

20.	These are the regions where you are allocated resources.  
![screnshot alt text](images/allregion.jpg).
21.	This is your Global account.  
![screnshot alt text](images/tech2018globalacct.jpg).

22.	These are your subaccounts.  
![screnshot alt text](images/opp363subacct.jpg).

23.	This is your Org.  
![screnshot alt text](images/opp363subCF.jpg).

24.	This is your space.  

![screnshot alt text](images/opp363space.jpg).
The number 397 will be different for you, it will be your student number.

- - - -
© 2018 SAP SE
- - - -
Previous Exercise: [Exercise 01 Setup](../Exercise-01-Setup) Next Exercise: [Exercise 3 - Publish Wishlist](../Exercise-03-Publish-Wishlist)

[Back to the Overview](../README.md)
