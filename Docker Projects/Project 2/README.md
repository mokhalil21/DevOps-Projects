# Project Description 


This Is A Docker Compose Project That Connects A Node.Js Application With Mongodb And Mongo Express. It Allows You To Run Multiple Services, Including Node.Js, Mongodb, And Mongo Express, By Simply Running A Docker Compose File. This Project Will Teach You How To Build An Application And Connect It To A Database Using Docker Compose.



To Understand The Benefits Of Compose File, We Should Know That Docker Compose Provides An Easy And Efficient Way To Manage And Run Multiple Containers. By Writing A Single Compose File, We Can Specify All The Configurations Related To Container Setup, Including Port Maps, Volume Maps, And Environment Variables. This Simplifies The Deployment Process As We Can Start Multiple Services With Just One Command, Making It Easier To Manage And Deploy Multiple Containers Simultaneously.

## Step 1 :
### Building the Compose File for the Node.js application

The first step is to create a Docker Compose file that defines the services we want to run. In this case, we need to run our Node.js application, MongoDB, and Mongo Express.

Here is an example of how to write the Docker Compose file syntax to run our Node.js application:


![1](https://user-images.githubusercontent.com/88173933/230984556-afcdba78-2672-4696-93fb-73a0883b2f28.png)


In this Docker Compose file, we define a service called "node-app" that builds the image from the current directory using the build command .

In the build command, the “.” specifies the build context for Docker to use when building the image.

 The build context is the set of files and directories located in the same directory as the Dockerfile.
So when you specify build: . in the Docker Compose file, it tells Docker to use the current directory (the location of the Docker Compose file) as the build context. It will then look for a Dockerfile in that directory and use it to build the image.

In summary, “build: . “ in the Docker Compose file tells Docker to build the Node.js application image using the Dockerfile in the current directory as the build context. 

 
And here is the docker file that docker compose will build the image from 


![2](https://user-images.githubusercontent.com/88173933/230984621-0ce6f966-30a1-4373-b22b-e83f1cb988cb.png)



We also specify a container name and map the container port 4000 to the host port 4000 using the ports command.

By running this Docker Compose file, we will be able to start our Node.js application and access it at localhost:4000.

------------


## Step 2 :
###  Adding MongoDB and Mongo Express to the Compose File

In this step, we will add MongoDB and Mongo Express to the Docker Compose file.

To add MongoDB to the Docker Compose file, we will use the official MongoDB image from Docker Hub.


![3](https://user-images.githubusercontent.com/88173933/230984692-af7afcbc-ddf7-49c2-9b53-973069571cbb.png)


 We will define a service called mongo and set the image to mongo.

 We will also set the MONGO_INITDB_ROOT_USERNAME and MONGO_INITDB_ROOT_PASSWORD environment variables to secure our MongoDB instance.

To add Mongo Express to the Docker Compose file, we will use the official Mongo Express image from Docker Hub. 

We will define a service called mongo-express and set the image to mongo-express. We will also map the default port 8081 of the container to the host port 8081. 

We will set the ME_CONFIG_MONGODB_ADMINUSERNAME, ME_CONFIG_MONGODB_ADMINPASSWORD, and ME_CONFIG_MONGODB_URL environment variables to allow Mongo Express to connect to our MongoDB instance.


------------

Here's an example of how to add MongoDB and Mongo Express to the Docker Compose file:


In this Docker Compose file, we define three services: node-app, mongo, and mongo-express.

 The mongo service uses the official MongoDB image and sets the MONGO_INITDB_ROOT_USERNAME and MONGO_INITDB_ROOT_PASSWORD environment variables.

 The mongo-express service uses the official Mongo Express image and maps its default port 8081 to the host port 8081.
 It also sets the ME_CONFIG_MONGODB_ADMINUSERNAME, ME_CONFIG_MONGODB_ADMINPASSWORD, and ME_CONFIG_MONGODB_URL environment variables to connect to the MongoDB instance.


![4](https://user-images.githubusercontent.com/88173933/230984771-b4e1e88a-2256-4ea7-828a-c1b861016209.png)


------------


To ensure that the MongoDB and Mongo Express services are started before the Node.js application service, we must ensure that the MongoDB container is up and running before the Node.js application container tries to connect to it. This can be achieved by adding the depends_on option in the Docker Compose file, which links the services and specifies the order in which they should start. By including the MongoDB and Mongo Express services in the depends_on section of the Node.js application service, we can ensure that those services are started before the Node.js application service.


This is the part where we specify the dependencies and the database for the Node.js app.



![5](https://user-images.githubusercontent.com/88173933/230984826-34d1ca06-6dd7-4e8a-afa0-38acf1f3308f.png)



------------

## Step 3 :


Before we proceed with building and running the three containers using the compose file, we need to install Mongoose, which is an Object Relational Mapping (ORM) library that enables Node.js applications to interact with MongoDB. After installing Mongoose, we can write a simple code in our Node.js application to establish a connection to the database.



To install Mongoose in our Node.js application, we need to use the Node Package Manager (npm) by running the following command in the terminal:

npm install mongoose 

This command will download and install the latest version of Mongoose from the official npm registry.



![6](https://user-images.githubusercontent.com/88173933/230984859-743753e1-11ef-4b34-897f-99e48514e188.png)


------------

## Step 4 :

After installing Mongoose, we can establish a connection to our MongoDB instance by calling the mongoose.connect() method. To accomplish this in our Node.js application, we need to first require the Mongoose module by adding the following code:

const mongoose = require('mongoose');


![7](https://user-images.githubusercontent.com/88173933/230984897-3ffa8610-8fab-47b5-82a7-74a300814403.png)



Next, we can connect to our MongoDB instance by using the following code:

const DB_USER = 'root';
const DB_PASSWORD = 'example';
const DB_HOST = 'mongo' ;
const DB_PORT = 27017 ;

const URI = mongodb://${DB_USER}:${DB_PASSWORD}@${DB_HOST}:${DB_PORT};
mongoose.connect(URI)
.then(() => console.log('Connected to database...'))
.catch((err) => console.log('Failed to connect to database:', err));

![8](https://user-images.githubusercontent.com/88173933/230984930-d4e9084a-64c8-492e-9b88-2bbac0a6d7ff.png)



------------



Now that we have all the necessary configuration in place for Docker Compose to build the image and deploy our three containers, all we need to do is execute the following command: docker-compose up -d –build .

 This command will read our Docker Compose file, and for each image and option specified, it will proceed to build them.


![9](https://user-images.githubusercontent.com/88173933/230984970-17764dfe-ca88-44c2-9e9c-70de933aa11c.png)



------------


To verify that all three containers are running, you can execute the following command: docker ps. This will display a list of all running containers, along with details such as the container ID, image used, and ports exposed. If all three containers are running successfully, you should see them listed in the output of this command.

![10](https://user-images.githubusercontent.com/88173933/230984999-a6506434-349b-4829-afac-23e68f5f455f.png)


------------

To check the running application, open your browser and navigate to http://localhost:4000. If the application is running successfully, you should be able to see the homepage or the landing page of the application.

![11](https://user-images.githubusercontent.com/88173933/230985103-fdf1fd8b-e00f-4827-aef5-f82feaaa3668.png)


------------
To check the running database, open your browser and navigate to http://localhost:8081. If the database is running successfully, you should see the homepage of the MongoDB management UI 


![12](https://user-images.githubusercontent.com/88173933/230985162-4d56d505-5be4-4b4e-bcb8-754f14e329c2.png)





