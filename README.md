## demo app - developing with Docker

This demo app shows a simple user profile app set up using 
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

### With Docker

#### To start the application

Step 1: Create docker network

    docker network create mongo-network 
![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/20912829-b566-4bbc-be01-3007d0bc0e80)

Step 2: start mongodb 

    docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo    

Step 3: start mongo-express
    
    docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express   

_NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit `--net` flag in `docker run` command_
![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/585234cc-ad17-49fa-990a-79b55562c770)
![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/a2febaf0-578d-4414-bb96-6e1060f47b4c)
![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/02a4ff48-e4f0-4864-8313-ce4cecf1906e)


Step 4: open mongo-express from browser

    http://localhost:8081
![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/e99a1d25-5db1-4a4f-a4c3-2258fe0b2c50)

Step 5: create `user-account` _db_ and `users` _collection_ in mongo-express
![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/4973ea35-8d64-4a69-8dd7-f9dce97b4440)
![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/eb03208d-f6c3-4dcc-8f45-4af61a6c206e)

Step 6: Start your nodejs application locally - go to `app` directory of project 

    cd app
    npm install 
    node server.js
    
Step 7: Access you nodejs application UI from browser

    http://localhost:3000
![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/c488040f-4a64-440c-b0cf-0c40f73e3325)

### With Docker Compose

#### To start the application

Step 1: start mongodb and mongo-express

    docker-compose -f docker-compose.yaml up
    
_You can access the mongo-express under localhost:8080 from your browser_
    
Step 2: in mongo-express UI - create a new database "my-db"
![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/2b6334e6-e301-4be1-8683-ea8b95e90a6a)


Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"       
    ![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/36bfb569-6232-4d8b-86ce-92560b216712)

Step 4: start node server 

    cd app
    npm install
    node server.js
    
Step 5: access the nodejs application from browser 

    http://localhost:3000

#### To build a docker image from the application

    docker build -t my-app:1.0 .       
    ![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/fd5c52f8-4538-41b3-9e80-17ce5f5903a6)
    ![image](https://github.com/ProtegeDpain/myCloudRepo/assets/102036335/36226f63-e78e-441c-a960-ec03ffa8a596)


The dot "." at the end of the command denotes location of the Dockerfile.
