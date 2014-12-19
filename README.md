Ansible Playbook to setup MongoDB Replica in Docker containers
---------------------------------



# Performing it manually

TODO: put the url here of the MongoDB instructions we are following

1.  Start the mongo db server

         docker rm mongo
         docker run --name mongo -v /home/core/mongo-files/data:/data/db -v /home/core/mongo-files:/opt/keyfile --hostname="db1.navabit.com" -p 27017:27017 -d mongo:2.6.5 --smallfiles

1. Launch a second container that can connect to the Mongo DB via the mongo cli.  This will launch an interactive shell

         docker run -it --link mongo:mongo --rm mongo:2.6.5 /bin/bash

1. Now you will be in the interactive shell of the container.  Run the mongo cli and connect to the first container that is actually running the container.
You might notice a lot of variables here.  Since we used the --link to the first container.  It gets all of the params.

From this containers shell.  Issue this command to connect into the first container's MongoDB server.

         mongo "$MONGO_PORT_27017_TCP_ADDR:$MONGO_PORT_27017_TCP_PORT/test"

1. Create users

         use admin
         db.createUser( {
             user: "siteUserAdmin",
             pwd: "1234",
             roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
           });


         db.createUser( {
             user: "siteRootAdmin",
             pwd: "1234",
             roles: [ { role: "root", db: "admin" } ]
           });

