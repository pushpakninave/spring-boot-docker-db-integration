# spring-boot-docker-db-integration
A Dockerized Spring Boot project for seamless SQL database connectivity, demonstrating how to configure and run a Spring Boot application with SQL database integration using Docker containers.

## Steps to do so:
(MySQL Docker + Spring Boot)

It walks through setting up a MySQL container in Docker and connecting it to a Spring Boot application. Ezing your development by running MySQL in a Docker container and makes it easy to connect to your application.

Steps to Set Up MySQL in Docker

### Step 1: Pull the MySQL Docker Image

First, pull the latest MySQL image from Docker Hub:

`docker pull mysql`

### Step 2: Run a MySQL Container

Now let’s create and run a container from the MySQL image. We’ll map MySQL’s default port (3306) to port 3308 on our local machine, set up a root password, and create a test database for our application.

`docker run -p 3308:3306 --name mysqlcontainer -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=testdatabase -d mysql`

Explanation of flags:

- `-p 3308:3306` : Maps port 3308 on your local machine to port 3306 in the container.
- `--name mysqlcontainer` : Names the container mysqlcontainer.
- `-e MYSQL_ROOT_PASSWORD=root` : Sets the root password to root.
- `-e MYSQL_DATABASE=testdatabase` : Creates a new database named testdatabase.
- `-d mysql` : Runs the container in detached mode.

### Step 3: Verify the Container is Running

To check if your MySQL container is running, use:

`docker ps`

You should see mysqlcontainer in the list of running containers, meaning MySQL is live and ready for connections.

Step 4: Create a Docker Network

To allow your Spring Boot application to connect to the MySQL container, let’s create a dedicated Docker network.

`docker network create mysqlnetwork`

This network will let our containers communicate easily, without requiring any extra configuration.

### Step 5: Connect the MySQL Container to the Network

Now we’ll add mysqlcontainer to the mysqlnetwork so that it’s accessible to other containers on this network.

`docker network connect mysqlnetwork mysqlcontainer`

Now, any other container on the mysqlnetwork can connect directly to mysqlcontainer.

Configuring Spring Boot to Connect to MySQL

In your Spring Boot project, open application.properties (or application.yml) and add the following database connection details:

```
spring.datasource.url=jdbc:mysql://mysqlcontainer:3306/testdatabase
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```
or 
> navigate to application.properties in current repository 

## ALL SET, IF YOU HAVE ANY ISSUE TRY RESOLVING IT YOURSELF IF NOT, CONTACT ME 
