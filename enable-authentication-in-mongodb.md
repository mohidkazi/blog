# Enable Authentication In MongoDB
![mongodb logo](https://webassets.mongodb.com/_com_assets/cms/mongodb_logo1-76twgcu2dm.png)
\
\
\
In This Tutorial we are gonna enable __Authentication__ by __Enabling Access Control__ on __MongoDB instance__.(By default MongoDB does not have any authentication system)

When accessing a MongoDB deployment that has access control enabled, users can only perform actions as determined by their roles.

## User Administrator
With __access control enabled__, Users will have to  access __MongoDB Instance__ using _username_ & _password_.
Every Users will be provided with __Roles__, Some <a name="builtInRoles">Built-In Roles</a> are

### Database User Role [¶](https://docs.mongodb.com/manual/reference/built-in-roles/#database-user-roles)
- [read](https://docs.mongodb.com/manual/reference/built-in-roles/#read):  
  Provides the ability to read data on all non-system collections
- [readWrite](https://docs.mongodb.com/manual/reference/built-in-roles/#readWrite):  
  Provides all the privileges of the [read](https://docs.mongodb.com/manual/reference/built-in-roles/#read) role plus ability to modify data on all non-system collections

### Database Administration Roles [¶](https://docs.mongodb.com/manual/reference/built-in-roles/#database-administration-roles)
- [dbAdmin](https://docs.mongodb.com/manual/reference/built-in-roles/#dbAdmin):  
  Provides the ability to perform administrative tasks such as schema-related tasks, indexing, and gathering statistics. This role does not grant privileges for user and role management.
- [dbOwner](https://docs.mongodb.com/manual/reference/built-in-roles/#dbOwner):  
  The database owner can perform any administrative action on the database. This role combines the privileges granted by the [readWrite](https://docs.mongodb.com/manual/reference/built-in-roles/#readWrite), [dbAdmin](https://docs.mongodb.com/manual/reference/built-in-roles/#dbAdmin) and [userAdmin](https://docs.mongodb.com/manual/reference/built-in-roles/#userAdmin) roles.
- [userAdmin](https://docs.mongodb.com/manual/reference/built-in-roles/#userAdmin):  
  Provides the ability to create and modify roles and users on the current database. Since the userAdmin role allows users to grant any privilege to any user, including themselves, the role also indirectly provides superuser access to either the database or, if scoped to the admin database, the cluster.

### Cluster Administration Roles [¶](https://docs.mongodb.com/manual/reference/built-in-roles/#cluster-administration-roles)
- [clusterAdmin](https://docs.mongodb.com/manual/reference/built-in-roles/#clusterAdmin):  
  Provides the greatest cluster-management access. This role combines the privileges granted by the [clusterManager](https://docs.mongodb.com/manual/reference/built-in-roles/#clusterManager), [clusterMonitor](https://docs.mongodb.com/manual/reference/built-in-roles/#clusterMonitor), and [hostManager](https://docs.mongodb.com/manual/reference/built-in-roles/#hostManager) roles. Additionally, the role provides the [dropDatabase](https://docs.mongodb.com/manual/reference/privilege-actions/#dropDatabase) action.

### Backup and Restoration Roles [¶](https://docs.mongodb.com/manual/reference/built-in-roles/#backup-and-restoration-roles)
- [backup](https://docs.mongodb.com/manual/reference/built-in-roles/#backup):  
  Provides minimal privileges needed for backing up data.
- [restore](https://docs.mongodb.com/manual/reference/built-in-roles/#restore):  
  Provides the necessary privileges to restore data from backups

### All-Database Roles [¶](https://docs.mongodb.com/manual/reference/built-in-roles/#all-database-roles)
- [readAnyDatabase](https://docs.mongodb.com/manual/reference/built-in-roles/#readAnyDatabase):  
  Provides the same read-only privileges as [read](https://docs.mongodb.com/manual/reference/built-in-roles/#read) on all databases.
- [readWriteAnyDatabase](https://docs.mongodb.com/manual/reference/built-in-roles/#readWriteAnyDatabase):  
  Provides the same privileges as [readWrite](https://docs.mongodb.com/manual/reference/built-in-roles/#readWrite) on all databases.
- [userAdminAnyDatabase](https://docs.mongodb.com/manual/reference/built-in-roles/#userAdminAnyDatabase):  
  Provides the same access to user administration operations as [userAdmin](https://docs.mongodb.com/manual/reference/built-in-roles/#userAdmin) on all databases.
- [dbAdminAnyDatabase](https://docs.mongodb.com/manual/reference/built-in-roles/#dbAdminAnyDatabase):  
  Provides the same privileges as [dbAdmin](https://docs.mongodb.com/manual/reference/built-in-roles/#dbAdmin) on all databases.

### Superuser Roles [¶](https://docs.mongodb.com/manual/reference/built-in-roles/#superuser-roles)
- [root](https://docs.mongodb.com/manual/reference/built-in-roles/#root):  
    Provides access to the operations and all the resources of the following roles combined:  
    - [readWriteAnyDatabase](https://docs.mongodb.com/manual/reference/built-in-roles/#readWriteAnyDatabase)
    - [userAdminAnyDatabase](https://docs.mongodb.com/manual/reference/built-in-roles/#userAdminAnyDatabase)
    - [dbAdminAnyDatabase](https://docs.mongodb.com/manual/reference/built-in-roles/#dbAdminAnyDatabase)
    - [clusterAdmin](https://docs.mongodb.com/manual/reference/built-in-roles/#clusterAdmin)
    - [backup](https://docs.mongodb.com/manual/reference/built-in-roles/#backup)
    - [restore](https://docs.mongodb.com/manual/reference/built-in-roles/#restore)

###### (Note:you can read more about it on mongodb documentation page)

## Procedure
### 1.Start MongoDB without access control.
Open your teminal and type following command for __Local__ Instance
```shell

ubuntu@your-pc:~# mongod --dbpath /var/lib/mongodb
```
or for your __Remote__ Instance
```shell

ubuntu@your-pc:~# mongod --host <your host name> --port 27017 --dbpath /var/lib/mongodb
```

### 2.Connect to the MongoDB instance.
Open you terminal and type following to connect to your __Local__ mongo shell
```shell

ubuntu@your-pc:~# mongo
```
or for your __Remote__ mongo shell
```shell

ubuntu@your-pc:~# mongo --host <your host name> --port 27017
```

### 3.Create the user administrator.
From the mongo shell, add a user with the [userAdminAnyDatabase](https://docs.mongodb.com/manual/reference/built-in-roles/#userAdminAnyDatabase) role in the admin database or you can add any role from MongoDB's [__Built-In Roles__](#builtInRoles).
But if you are creating user for the first time, go with [userAdminAnyDatabase](https://docs.mongodb.com/manual/reference/built-in-roles/#userAdminAnyDatabase).

First select __admin__ database
```shell
> use admin
```
then run following command where _<username>_ is any name
```shell
> db.createUser(
    {
      user: "<username>",
      pwd: passwordPrompt(), // or <password>
      roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
    }
  )
```
_passwordPrompt()_ will ask for password after you hit enter

### 4.Re-start the MongoDB instance with access control.
Shut down the mongod instance from admin database.
```shell
> db.adminCommand( { shutdown: 1 } )
```
or
```shell
> db.shutdownServer()
```

After then you will see `server should be down...`, which means everything went well.
Now type to exit the mongo shell.
```shell
> exit
```

Now, from your ubuntu terminal, type following command to add the security.auth or security.authorization to the MongoDB config file.
```shell
ubuntu@your-pc:~# sudo vi /etc/mongod.conf
 ```
 or
 ```shell
ubuntu@your-pc:~# sudo nano /etc/mongod.conf
 ```
 
 prior to version 4.x, it may look something like
 ```shell
# Turn on/off security.  Off is currently the default
#noauth = true
#auth = true
 ```
just uncomment it like this
```shell
# Turn on/off security.  Off is currently the default
#noauth = true
auth = true
```
Or if you are using version greater or equal to 4.x, enable __authorization__
```shell
security:
 authorization: enabled
```
From your terminal, restart your __MongoDB__ instance
```shell
ubuntu@your-pc:~# sudo systemctl restart mongodb
```
or if you have installed mongodb driver directly from mongodb website instead of ubuntu snap store, then type this command instead
```shell
ubuntu@your-pc:~# sudo systemctl restart mongod
```

Now check your __MongoDB__ instance
```shell
ubuntu@your-pc:~# sudo systemctl status mongodb
```
or
```shell
ubuntu@your-pc:~# sudo systemctl status mongod
```
you should see something like this
```shell
Active: active (running)
```
### 5.Connect to MongoDB instance with superAdmin access.
```shell
ubuntu@your-pc:~# mongo --authenticationDatabase "admin" -u "<username>" -p
```
once you press enter, you'll get password prompt, just enter the password
```shell
MongoDB shell version v3.x.x
Enter password: <password>
```
######(You can also/should create multiple users for specific database)
### 6.Create user access for specific database
We'll create user with only __read write__ access
```shell
use <your-db-name>
db.createUser({
user: "<username>",
pwd: "<password>",
roles: ["readWrite"]
})
```
or
```shell
db.createUser({
user: "<username>",
pwd: "<password>",
roles: [{"readWrite", db: "<your-db-name>"}]
})
```
### 7.Connect to specific MongoDB instance with limited access.
```shell
ubuntu@your-pc:~# mongo --authenticationDatabase "<your-db-name>" -u "<username>" -p
```
and then enter your password which i showed you in __step 5__.

That's it for today...
