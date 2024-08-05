# Dockerized ecommerce   

### Installation  
**Download the latest version of Docker Desktop**
[https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)  
Select the platform to install it on. Follow the install instructions.

**(Optional) Check if docker and docker-compose are installed.**  
```bash
docker --version
```
```bash
docker-compose --version
```
**Clone the docker repo to your "Projects" folder**
**Rename .env_copy to .env**  
Add your credentials to the appropriate variables.
```.env
# exapmple
MYSQL_ROOT_PASSWORD=your_root_password
MYSQL_USER=your_mysql_username
MYSQL_PASSWORD=your_mysql_password
PATH_TO_PROJECT_DIR=../
```  

**Add 00-init.php file to ./{site folder}/dist/config/ use the credentials added in the .env file**
**In 00-int.php file change $_['db_host'] = 'localhost' to $_['db_host'] = 'mysql'**

**Add sql dump files to ./install in the docker folder**  

**Where you have your PHP installed on your computer, you may need to uncomment the following in your php.ini file.** 
Uncomment in your php.ini file.
```bash
extension=openssl
extension=curl
extension=fileinfo
extension=gd
extension=zip
```

You may also need to add disable-tls=true at the bottom.
```bash
disable-tls=true
```

**(On initial setup. Skip if already done) cd into /{site folder}/dist/**
Install composer dependencies 
```bash
composer install
```

**cd into the root directory the directory with the file _docker-compose.yml_ file in it.**  
```bash
docker-compose up -d --build
#or 
docker compose up -d --build
```
Allow the database to finish populating. Depending on the size of the dumps this can take 30+ minutes.

**The configuration of virtual hosts may vary among different operating systems;**

**Windows** users the hosts file is located at c:\Windows\System32\Drivers\etc\hosts. Right click on Notepad in your start menu and select “Run as Administrator”. This is crucial to ensure you can make the required changes to the file.  

**Linux** users, the hosts file is located at: /etc/hosts directory. The instructions below are valid for Linux distribution, including Ubuntu, CentOS, RHEL, Debian and Linux Mint. When prompted enter your sudo password.  

**Mac** users can find the hosts file in the /private/etc/hosts directory. You can edit it with any text editor as long as you have root user privileges. Important!  

**In the .host file add:**
```bash
127.0.0.1 buckedup.local
127.0.0.1 bootcamp.local
127.0.0.1 brandloudr.local
127.0.0.1 test.local
127.0.0.1 phpmyadmin.local
```
**You should be all set up now. Use the URL**  
For buckedup.local http://buckedup.local  
For brandloudr.local http://brandloudr.local  
For bootcamp.local http://bootcamp.local  
For phpmyadmin.local http://phpmyadmin.local  
For test.local http://test.local 

**You may have to run these sql:**

```sql
-- ecommerce db
UPDATE `sites` SET 
`domain` = 'buckedup.local', 
`admin_domain` = 'buckedup.local', 
`cookie_domain` = '.buckedup.local' 
WHERE `sites`.`id` = 1;

-- bootcamp db
UPDATE `bootcamps` SET `domain` = 'bootcamp.local' WHERE `bootcamps`.`id` = 1;

-- brandloudr db
UPDATE `apps` SET `domain` = 'brandloudr.local' WHERE `apps`.`id` = 1;

```


**After initial installation you just need you can just run**  
```bash
docker-compose up -d
#or 
docker compose up -d
```
to start it up and

```bash
docker-compose down
#or 
docker compose up -d
```
to shut it down

### Reinstalling your database.   
**If you need to reinstall your database run**
```bash
docker-compose down --rmi "all" -v
#or 
docker compose down --rmi "all" -v
```  
This command will remove all docker containers, images, and volumes.  

**Add or replace the msql dumps for you database you need.**  
next  
```bash
docker-compose up -d --build
#or 
docker compose up -d --build
```
Allow the database to finish populating.  

**The default admin login is**
```
admin@buckedup.com
admin
```

## Commands to know:
```
# Starts existing containers for a service.
docker-compose start

# Stops running containers without removing them.
docker-compose stop

# Pauses running containers of a service.
docker-compose pause

# Unpauses paused containers of a service.
docker-compose unpause

# Lists containers.
docker-compose ps

# Builds, (re)creates, starts, and attaches to containers for a service. Adding -d or --detach will run docker in the background
docker-compose up

# Stops containers and removes containers, networks, volumes, and images created by up.
docker-compose down

# To see all running containers
docker ps

# To get inside a running container
docker exec -it CONTAINERNAME/CONTAINERID bash
```