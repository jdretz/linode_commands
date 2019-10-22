# MongoDB Set Up on Ubuntu 18.04
1. `$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4` # GPG Key
2. `$ sudo echo "deb http://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list` # Create needed files
3. `$ sudo apt-get update` # Reload packages
4. `$ sudo apt-get install -y mongodb-org` # install MongoDB
5. `$ sudo mkdir -p /data/db` # Create the db files
6. ```$ sudo chown -R `id -un` /data/db``` # Give appropriate permissions to directories
7. `$ sudo systemctl start mongod` # Start mongod process
8. `$ sudo systemctl enable mongod` # Enable the process
9. `$ sudo netstat -plntu` # Have mongod start on boot
10. `$ sudo systemctl stop mongod` # Stop process
11. `$ mongod --port 27017` # Start process to ensure it's running on port 27017
12. Open a new tab, ssh into remote server to access mongo shell --> `$ mongo --port 27017` 
13. (Now in the mongo shell) `> use admin` [these commands come from authentication documentation](https://docs.mongodb.com/manual/tutorial/enable-authentication/) # Access admin database
14. `> db.createUser({ user: "username", pwd: passwordPrompt(), roles: [{ role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]})` # Create superuser for all databases
15. `>db.adminCommand( { shutdown: 1 } )` # Stop mongod to change config
16. `>exit` # Leave mongo shell
17.`$ sudo nano /etc/mongod.conf ` # Open config file to enable auth
18. Uncomment the security config, and type `authorization: enabled` on line below. Match format to other config options.
19. Save (Ctl+X), Accept (y) and exit (Enter)
20. `$ mongod --auth --port 27017` # Start mongod process with auth enabled (this would be in done in the tab that mongod was logging to in previous steps)
21. `$ mongo --port 27017  --authenticationDatabase "admin" -u "myUserAdmin" -p` # Access database as authenticated user
22. `>use [new database name]` # create a new database
23. `> db.createUser({ user: "username", pwd: passwordPrompt(), roles: [{ role: "readWrite", db:"dbName"}]})` # This is just an example from the documentation showing how one could create a user, for a new database, that didn't have as many permisssions as previous admin user.

The database needs a document (I believe) in order to be saved, so make sure a holder document is inserted until connection with the app can be confirmed. (`>db.[collection name].insert({})`)
