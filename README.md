Ansible Playbook to setup MongoDB Replica in Docker containers
---------------------------------



# Performing it manually

TODO: put the url here of the MongoDB instructions we are following

1.  Start the mongo db server

         docker rm mongo
         docker run --name mongo -v /home/core/mongo-files/data:/data/db -v /home/core/mongo-files:/opt/keyfile --hostname="db1.navabit.com" -p 27017:27017 -d mongo:2.6.5 --smallfiles

1. Launch a second container that can connect to the Mongo DB via the mongo cli.  This will launch an interactive shell

         docker run -it --link mongo:mongo --rm mongo:2.6.5 /bin/bash

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

