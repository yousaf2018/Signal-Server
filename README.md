### Signal-Server-Deployment-Documentation

* There is no official set up guide available for signal server deployment. 
* I got help from unofficial signal community forum https://community.signalusers.org/ for server code building.
* Below is the complete path for signal server code building

### Building Signal Server Code follow the below steps
* Linux Mint 19.3 Cinnamon(Any other linux distrubtion will also work)
* Clone the latest source code from official signal server github repository 
```
    git clone https://github.com/signalapp/Signal-Server 
```
* Install Java(11.0.11) from official oracle website by creating account with oracle
* Remove all other java versions from your system because it will create some dependency issues during signal source code building 
* After successfull installation of java(11.0.11) run the below commands one by one
```
    sudo add-apt-repository -y ppa:webupd8team/java
    sudo apt-get update 
    sudo apt-get install -y oracle-java8-installer
    sudo apt-get install -y oracle-java8-unlimited-jce-policy 
```
* Run the following commands for installation of Radis
```
    sudo apt-get install -y redis-server
  
```
* Database Installation with creation of root user 
```
    sudo apt-get install postgresql postgresql-contrib -y
    sudo -i -u postgres
    createdb accountdb
    createdb messagedb 
    createuser --interactive
    psql
    ALTER USER "Signal" WITH PASSWORD 'Signal!!';
```
* Open your terminal and run the below commands with little modification according to your system and edit files with values
```
    gedit /etc/postgresql/10(It will be according to verison)/main/postgresql.conf
    
    Below is the requried changes in file
    * listen_addresses='localhost' ------> listen_addresses='*'

    gedit /etc/postgresql/10(It will be according to verison)/main/pg_hba.conf
    Below is the requried changes in file
    * Add the line in file -------> host all all * md5
```
* After successfull editing in the files run the below command for restart the databases
```
    invoke-rc.d postgresql restart

```
* If you are done with all steps than now enter to latest cloned directory from github by using command cd Signal-Server
* Below is the command for building Signal Server Code 
```
    mvn install -DskipTests	

```

