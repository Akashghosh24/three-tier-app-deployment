# Three Tier App Architecture and Deployment
### Introduction
We have used a Three Tier Node JS app to understand how exactly a three tier app functions, gets build,containerised and deployed on K8s.
Once we understand a three tier deployment, the same concept can be extended to large scale applications running multiple microservices.

### Let's understand first, what exactly Three Tier App means?
-	A three-tier application architecture is a client-server architecture that has a presentation tier (aka web tier), a logic tier (aka application tier) and a data tier (aka database tier).
-	The Web/Presentation tier is a graphical user interface that communicates with the other two tiers through API calls. So the code which is responsible for website GUI and interface is part of the Presentation Tier.
-	The Logic/Application tier is written is a programming language and handles business logic that supports the application’s core functions. This is the core of the application as this is where the App Logic is defined.
-	The database tier The data tier consists of a database and a program for managing read and write access to a database. Here the App data eg. user details are stored in a database that can be fetched by the App Tier.

 ![image](https://github.com/Akashghosh24/three-tier-app-deployment/assets/94949101/226de36b-c1f8-463d-baed-0e8a59d3ff01)

# Yelp Camp Web Application
Since we now understand what a three-tier-app means, we will now understand the build and functionality using a Node JS Project - Web App.
This web application allows users to add, view, access, and rate campgrounds by location. It is based on "The Web Developer Bootcamp" by Colt Steele, but includes several modifications and bug fixes. The application leverages a variety of technologies and packages, such as:

- Node.js with Express: Used for the web server.
- Bootstrap: For front-end design.
- Mapbox: Provides a fancy cluster map.
- MongoDB Atlas: Serves as the database.
- Passport package with local strategy: For authentication and authorization.
- Cloudinary: Used for cloud-based image storage.
- Helmet: Enhances application security.

### Understanding the Functionality:
- The function of Web App is to list camp, upload images, mark it on Map, add rating and view existing rating.
- Here we will also create users that will sign in. So all the textual data will be stored in a DB. We are using MongoDB in our case which will be DB tier for us.
We can also use DB installed locally but we are using DB as a service to avoid installation and maintenance. In any three tier architecutre, we can use SQL Server hosted on Azure or DB PaaS service.
We just need to mention the connection details at the Logical Tier to specify the DB being used.
- We are going to use third party resources namely- Cloudinary - To store the Camp Images and Stuff, Mapbox- to Store Map Data. So we also need to add the connection strings in the App Tier.

### Understanding the Folder Structure of the Application Source Code:
This is a Node JS based application so the folder structure is applicable only for NodeJS based projects.
 
 ![image](https://github.com/Akashghosh24/three-tier-app-deployment/assets/94949101/dca34d14-3dbb-4bdb-9c15-abbc8db115cc)

- The Front End of the Application will be residing in the Public and Views Folder. Contains static assets such as images, CSS, JavaScript files, fonts, and other files that need to be accessible directly by the client's browser.
- The Backend Data is stored in controllers, models, routes, utils, seeds, schemas.js, and app.js files and folder. All the connction string for DB, Third Party Apps are integrated here.
- Environment File- We also have .env file that contains the environment variables. The app tier will have variables being used for connection string of DB, third party apps. So at this is where we mention the connection strings which can be used with backend. Make sure the .env file is in app.js folder.
- package.json contains information about the project, such as its name, version, author, and license, as well as a list of dependencies and scripts needed to run, build, and test the project.
- package-lock.json is an automatically generated file that records the exact versions of all installed dependencies and their nested dependencies in a Node.js project. This file ensures that the project can be reproduced exactly as it was during the last successful installation, providing consistency and reliability across different environments and installations.

### Setup Instructions
To get this application up and running, you'll need to set up accounts with Cloudinary, Mapbox, and MongoDB Atlas. Once these are set up, create a .env file in the same folder as app.js. This file should contain the following configurations:

- CLOUDINARY_CLOUD_NAME=[Your Cloudinary Cloud Name]
- CLOUDINARY_KEY=[Your Cloudinary Key]
- CLOUDINARY_SECRET=[Your Cloudinary Secret]
- MAPBOX_TOKEN=[Your Mapbox Token]
- DB_URL=[Your MongoDB Atlas Connection URL]
- SECRET=[Your Chosen Secret Key] # This can be any value you prefer


To get the above data:
- Cloudinary Connection Strings can be retrieved from Creating a account in Cloudinary>Account> Settings>Proudct environmnet settings> API keys.
![image](https://github.com/Akashghosh24/three-tier-app-deployment/assets/94949101/6b1e9814-617d-4535-8039-556c520e3cca)

- For Map box, Create account in Mapbox>Account>Access Tokens
 ![image](https://github.com/Akashghosh24/three-tier-app-deployment/assets/94949101/19a7c12a-a3fd-4cd4-b3df-d0a70b5581ad)

- For MongoDB , create an account in MongoDB. Project> Data Services Tab> Application Development> Connect to Cluster> Add Connection String
 ![image](https://github.com/Akashghosh24/three-tier-app-deployment/assets/94949101/ac21b8f9-2fe2-4d95-8e64-c8e1d1efe131)
Once we have all the configuration data, we can start with the build.

### Deployment Strategy:
- The App Will be first build locally to understand it's build process.
- Then the App will be deployed on Containers via Pipeline
- Finally Once Production Ready, it will be deploye to AKS via pipeline.

### Infra details
To build the app locally, we will run in on Ubuntu VM and for Pipeline we will run it via Self Hosted Agent.
For running the app make sure the NSG rules are allowed for the ports- 3000, 8080, 
Make sure the Local machine and self hosted agent has NPM installed to run the build.
The Infra shell script is and necessary files are in Infra Folder.
The App Source Code and necessary files are in App Folder.
