# Furniture Shop Documentation
## This repository is for TechEd 2018 hands-on session OPP363
## Purpose of this Hands-on Session
The purpose of this Hands-on session is to provide a deeper understanding of developing, deploying and operating cloud-native applications in the [Cloud Foundry environment of SAP Cloud Platform](https://cloudplatform.sap.com/enterprise-paas/cloudfoundry.html).
## Introduction to SAP Cloud Platform Cloud Foundry Environment

[Cloud Foundry](https://www.cloudfoundry.org/) is an open source Platform-as-a-Service (PaaS) technology with broad industry support. [SAP Cloud Platform Cloud Foundry environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/ab512c3fbda248ab82c1c545bde19c78.html#9c7092c7b7ae4d49bc8ae35fdd0e0b18.html) provides the benefits of the open source Cloud Foundry technology along with several, differentiating enterprise-grade features and functionalities.

A key design principle of Cloud Foundry is to build applications as scalable, stateless microservices that utilize various backing services for persistence, messaging, etc.

Microservices can be developed in practically any programming language as long as there is a corresponding Cloud Foundry buildpack. SAP Cloud Platform provides in-built support for certain buildpacks such as Java and Node.js and allows use of any other community buildpacks.

SAP Cloud Platform includes several backing services including the flagship SAP HANA as well as other popular open source services such as PostgreSQL, RabbitMQ and Redis.

In addition, the Cloud Foundry environment of SAP Cloud Platform includes various other technical services such as Connectivity, AutoScaling, Security and Job Scheduler.

## Runtimes / services used in the hands-on
The exercises in the current hands-on utilize the following runtimes:
- Java
- Node.js
- HTML5

For the current hands-on, various backing and technical services are used including:
- SAP HANA
- PostgreSQL
- RabbitMQ
- Connectivity
- Destination
- Authorization & Trust Management (xsuaa)
- Application Logging
- Application Autoscaler

## Tools used in the hands-on
For application development and deployment, this hands-on uses the recently launched, powerful, web-based tooling - [SAP Web IDE Full-Stack](https://cloudplatform.sap.com/capabilities/technical-asset-info.SAP-Web-IDE-Full-Stack.52fdf566-8709-41ef-bfa4-2aabcd33a865.html).

In particular, this hands-on uses the following capabilities of the SAP Web IDE Full-Stack:
- [Application Programming Model](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/00823f91779d4d42aa29a498e0535cdf.html) which allows developers to focus on domain logic by providing integrated frameworks for data, service and user interface layers
- [Developing Multi-Target Applications](https://help.sap.com/viewer/825270ffffe74d9f988a0f0066ad59f0/CF/en-US/a71bf8281254489ea8be6e323199b304.html) which enables holistic life cycle management of application modules aimed at disparate runtimes, and various underlying services
- [Connect to Cloud Foundry services](https://help.sap.com/viewer/825270ffffe74d9f988a0f0066ad59f0/CF/en-US/39a1e84313ec44248aa5536142633636.html) and consume them from the applications
- [Using Source Control (Git)](https://help.sap.com/viewer/825270ffffe74d9f988a0f0066ad59f0/CF/en-US/4eddb4cfc29946f6b059306cbdfcb392.html) for connecting and interacting with the remote repositories

## Hands-on Scenario
![Hands-on scenario](/Overview/images/Hands-onScenario.JPG)

In order to elucidate the capabilities and benefits of the Cloud Foundry environment of SAP Cloud Platform, we have chosen a simple but modern business scenario for this hands-on exercise.

Think of a furniture shop business that wants to change the process of deciding which items are added to the shop. Instead of arbitrarily deciding the items in the shop, Franck (the person in charge of the department) , wants to take the following approach:
- First, create and publish a Wishlist of items he (Franck) would like to see in the shop
- Seek rating and comments from customers (like Mary in our scenario) for assessing the popularity of the items
- Franck to prioritize the items, their quantities, etc., for placing an Order

## Application Design

![Application Architecture](/Overview/images/ApplArchitecture.JPG)

To realize the above scenario, the following microservices will be built.

### Wishlist and Ordering service
First, we will have a Wishlist service for Franck to publish his Wishlist. This application will be built using:
- Application Programming Model of SAP Cloud Platform using SAP Web IDE Full-Stack
- For data persistence, this application will utilize SAP HANA
- For the front-end, this application will use SAPUI5 templates, available as a SAP Web IDE Full-stack capability.

Next, we will build upon the Wishlist service to add Ordering capabilities, for which, it is required to fetch certain data, such as product price, from on-premise backend systems. In order to connect to the backend system, this step will involve consuming various technical services from SAP Cloud Platform Cloud Foundry environment such as - connectivity, destination and xsuaa.

### Rating and Tweet Services
In order to seek ratings from customers like Mary and also involve additional customers via social channels, we will build a couple of services.

First, we will have a Node.js based Ratings service which uses
- A simple front-end using a SAPUI5 template, for Mary to provide her ratings / comments
- PostgreSQL backing service for persisting the ratings / comments.

To engage other customers and seek greater customer input for rating the items, we will add a Tweet service that posts a message on the store's twitter account whenever a customer (like Mary) reviews any item in Franck's Wishlist. This service is also built using Node.js. For the communication between the Ratings service and the Tweet service, we will use RabbitMQ backing service.


## Exercises

- [Exercise 01 - Setup/System Perparation](Exercise-01-Setup)
- [Exercise 02 - What is Org and Space on CF](Exercise-02-What-is-OrgandSpace-CF)
- [Exercise 03 - Publish Wishlist](Exercise-03-Publish-Wishlist)
- [Exercise 04 - Order New Items](Exercise-04-Order-New-Items)
- [Exercise 05 - Logging](Exercise-05-Logging)
- [Exercise 06 - Comments and Ratings Backend](Exercise-06-Comments-and-Ratings-Backend)
- [Exercise 07 - Comments and Ratings Frontend](Exercise-07-Comments-and-Ratings-Frontend)
- [Exercise 08 - Tweet Comments Backend](Exercise-08-Tweet-Comments-Backend)
- [Exercise 09 - Test Order New Items with User Input](Exercise-09-Test-Order-New-Items-with-User-Input)
- [Exercise 10 - Autoscaling of Comments and Ratings](Exercise-10-Autoscaling-of-Comments-and-Ratings)
- [Exercise 11 - Blue-Green Deployment of Comments and Ratings](Exercise-11-Blue-Green-Deployment-of-Comments-and-Ratings)
- [Exercise 12 - Monitoring](Exercise-12-Monitoring)
- [Exercise 13 - Debugging](Exercise-13-Debugging)



## License
This project is licensed under the SAP SAMPLE CODE LICENSE AGREEMENT except as noted otherwise in the [LICENSE](./LICENSE) file.
