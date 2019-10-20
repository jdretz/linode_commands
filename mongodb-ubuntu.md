# MongoDB Set Up on Linode (Ubuntu 18.04)
1. `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4`
2. `sudo echo "deb http://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list`
3. `sudo apt-get update`
4. `sudo apt-get install -y mongodb-org`
5. `sudo systemctl start mongod`
6. `sudo systemctl enable mongod`
7. `sudo netstat -plntu`
8. Before you can start mongod process.. `sudo mkdir -p /data/db`
9. ```sudo chown -R `id -un` /data/db```
10. `mongod --port 27017` [these commands come from documentation](https://docs.mongodb.com/manual/tutorial/enable-authentication/)
11. `mongo --port 27017` (in new tab, may need to ssh into remote again) 
12. Now in the mongo shell `> use admin`
13. `> db.createUser({ user: "username", pwd: passwordPrompt(), roles: [{ role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]})`
14. `>db.adminCommand( { shutdown: 1 } )`
15. In other tab, (where mongo was running)`sudo nano /etc/mongod.conf `
16. Uncomment the security config, and type `authorization: enabled` on line below. Match format to other config options
17. Still in that other tab `mongod --auth --port 27017`
18. `exit` shell and restart shell `mongo --port 27017  --authenticationDatabase "admin" -u "myUserAdmin" -p`
19. `>use [new database name]`
20. These are example permissions form documentation. There are more, and multiple roles can be assigned. `> db.createUser({ user: "username", pwd: passwordPrompt(), roles: [{ role: "readWrite", db:"dbName"}]})`
The database needs a document (I believe) in order to be saved, so make sure a holder document is inserted until connection with the app can be confirmed.
