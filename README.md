# Ranger Installation using Cloudera Manager

## Pre-Requisites 

* Install a Database or use existing one (MySql, Postgrace)
* Install Infra Solr (for audits)
# PART I

#### 1)Install Mysql Server 

![ab33d861-f5cf-47a5-ad5f-8ba36b428493](https://user-images.githubusercontent.com/124764525/217611823-8d2a199d-4b61-4ae6-98fb-e20f2a3d4e8c.jpg)
```
yum install -u mysql -server
service mysqld start
chkconfig mysqld on
```

#### 2)Make sure you have the MYSQL connector 
Version should be 5.7 or higher in the /usr/share/java/ directory with name mysql-connector-java.jar.
If not avaliable, use following command to install the connector.
```
yum install -y mysql-connector-java*
```

#### 3)Edit the following file: /etc/my.cnf and add the following line:
```
log_bin_trust_function_creators=1
```
#### 4)Restart the database:
```
systemctl restart mysqld
```

#### 5)Log in to mysql:
```
mysql -u root -p
```
#### 6)Run the following commands to create the Ranger Database and User & Grant this new user with required permissions.
```
CREATE DATABASE rangerdb;
CREATE USER 'rangeradmin'@'%' IDENTIFIED BY 'Cloudera123'; 
CREATE USER 'rangeradmin'@'localhost' IDENTIFIED BY 'Cloudera123';
CREATE USER 'rangeradmin'@'<Ranger Admin Role hostname>' IDENTIFIED BY 'Cloudera123';
GRANT ALL PRIVILEGES ON rangerdb.*  TO 'rangeradmin'@'%';
GRANT ALL PRIVILEGES ON rangerdb.* TO 'rangeradmin'@'localhost';
GRANT ALL PRIVILEGES ON rangerdb.* TO 'rangeradmin'@'<Ranger Admin Role hostname>';
FLUSH PRIVILEGES;
```
#### 7) Use the exit; command to exit MySQL.

#### 8) Test connecting this new user to the database using the following command:

     mysql -u rangeradmin -p

#### 9) After testing the connection, exit MySQL.

#### 10) Continue with the cluster installation or upgrade to complete the transition.


# PART II : Install Ranger

#### 1)Go to Cloudera Manager Dashboard --> Add Service --> Continue
![f272d509-7727-4392-84b1-94cfcb94cf1a](https://user-images.githubusercontent.com/124764525/217615233-e07887c0-a948-4eaf-ba3b-2410cc11e5d6.jpg)

#### 2)Choose Services --> Select Ranger, InfraSolr

![84e6749f-0595-4064-842c-89a06bc19ef3](https://user-images.githubusercontent.com/124764525/217615376-31fe0da2-8ca4-4ee4-aee4-5bddc8e52062.jpg)

#### 3)Assign Masters & Slaves --> Select host for Ranger admin & Ranger User Sync & Ranger Tag Sync --> Continue

![24420614-834c-4e6e-8258-f2297f582d84](https://user-images.githubusercontent.com/124764525/217615535-5d377545-a28d-4573-937d-fbda589dee42.jpg)

#### 4)Customize Services & update the necessary information (make sure port numberer of sql is 3306 ) --> Test Connection --> Continue

![23d8273a-c030-4a73-a848-e4dbf0b9ad1b](https://user-images.githubusercontent.com/124764525/217615623-7e890eb0-510f-4399-92af-e984189b11f9.jpg)

#### 5)Review Changes --> Continue
![1f3200e6-fa3a-43d3-b724-3e5c367c3d3b](https://user-images.githubusercontent.com/124764525/217615734-345d2289-2ee0-4bde-9d3f-91d5894f5b11.jpg)

#### 6) Click Finish to deploy 

![f460902c-4d89-46a2-9314-7dd698310e67](https://user-images.githubusercontent.com/124764525/217615817-a35560c8-0253-4e8d-912b-35b44de7df32.jpg)



