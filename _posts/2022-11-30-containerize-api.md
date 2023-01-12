---
layout: post
title: "Create a Container for Spring Boot/MySQL Application"
author: skylar_lynner
categories: [ java, docker ]
featured: true
---

### Project Context

Docker will need to be installed to create the application container.
It can be downloaded from [here](https://docs.docker.com/get-docker/).
Creating an account and logging into the application is recommended.

The sample project referenced in this post can be found
[here](https://github.com/oneexists/containers).

The Spring Boot application requires three environment variables in
order to make a connection to the MySQL database. Their values are:
  ```
  CONTAINERS_DB_URL=jdbc:mysql://containers-db:3306/containers
  CONTAINERS_DB_USERNAME=root
  CONTAINERS_DB_PASSWORD=password
  ```

In three steps, we will create:
- A Docker image of the Spring Boot application using Maven
  (named `containers` with the tag `spring-boot`)
- Two Docker volumes to manage MySQL (`containers_data` and `containers_config`),
  which will connect the application's data to local storage
- A Docker network to connect MySQL to the Spring Boot application
  (`containers_net`)
- Two Docker containers to run the MySQL and Spring Boot application
  instances (`containers-db` and `containers-api`)

### Step 1: Create Spring Boot Image

The `pom.xml` file includes the image configuration in the `plugins`
section. It uses [Google Jib](https://cloud.google.com/blog/products/application-development/introducing-jib-build-java-docker-images-better)
to assist with layering the application to minimize its size.

Use Maven in the terminal to package the application and build the
image:
```
./mvnw package -DskipTests spring-boot:build-image
```

Execute the command `docker images` to confirm the image exists. The
images for `paketobuildpacks/run` and `pakettobuildpacks/builder`
will appear along with the newly created `containers` image.

#### Breakdown

- `containers:spring-boot` represents the image's name and tag
- the application is packaged using configuration in the `pom.xml` and
  Maven in the terminal to create a Docker image of the application

### Step 2: Creating the MySQL Container

Docker volumes will be used to store the data and configuration of 
the database using the commands:
```
docker volume create containers_data
docker volume create containers_config
```

The containers will communicate using a Docker network that can be
created using:
```
docker network create containers_net
```

Next, create a container from the MySQL image (replace `password` with the 
password you would like to use for the database):
```
docker run -it -d -v mysql_data:/var/lib/mysql -v containers_config:/etc/mysql/conf.d --network containers_net --name containers-db -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 mysql
```

This is a good time to initialize the database. First access the 
database inside the container:
```bash
docker exec -ti containers-db bash
```
Then sign into MySQL and enter the database password when prompted:
```
mysql -u root -p
```
The database can be created using the following SQL statement:
```
create database containers;
```

There is a schema included in `sql/schema.sql` that creates a 
testing database. To use this, update the database name at the 
end of the environment variable to `containers_test` and initialize
the schema inside the Docker container using the following command:
```bash
docker exec -i containers-db mysql -u root -p"$CONTAINERS_DB_PASSWORD" < sql/schema.sql
```

#### Breakdown

- MySQL data is managed using two Docker volumes (`containers_data` and
  `containers_config`)
- The application containers will communicate using a Docker network
  (`containers_net`)
- The database is managed in the container `containers-db` using the
  `mysql` image (provided from Docker Hub), it uses the volumes
  for its data, the `containers_net` network for communication on port `3306`,
  and uses the the `root` login
- After the container is created, the database is initialized using 
  `docker exec` to access MySQL within the `containers-db` instance
  and the test database can be initialized within the container as well

### Step 3: Create the API Container

The second container can be created for the Spring Boot application
(again, replacing `password` to match the password used to create
the database):
```
docker run -d --name containers-api --network containers_net -e CONTAINERS_DB_URL=jdbc:mysql://containers-db:3306/containers -e CONTAINERS_DB_USERNAME=root -e CONTAINERS_DB_PASSWORD=password -p 8080:8080 containers:spring-boot
```

With both of the containers running, the application will be available
at [this endpoint](http://localhost:8080/api) and return a 403 Forbidden 
response.

#### Breakdown

- The container is created from the `containers:spring-boot` image 
  with the name `containers-api`
- It uses the `containers_net` network to communicate with the 
  database with the environment variables provided and exposes port 
  `8080`
- The application will provide a `403 Forbidden` response at its
  endpoint if accessed without a JWT token [here](http://localhost:8080/api)

### Sending an HTTP Request

An account can be created by sending a request to the application.
The request can be executed using REST Client in VS Code by using the
file `requests.http` containing:
{% raw %}
```
@url = http://localhost:8080

POST {{url}}/api/appUsers HTTP/1.1
Content-Type: application/json

{
  "username": "my-username",
  "password": "P@ssw0rd!"
}
```
{% endraw %}

The same request body can be sent to `http://localhost:8080/authenticate`
to receive a JWT token. Use this token by adding it to the `@jwt`
reference at the top of the `requests.http` file. This will use the  
token to view the users endpoint at `http://localhost:8080/api/appUsers`
with the request:
{% raw %}
```
@jwt = <your.jwt.here>

...

GET {{url}}/authenticate HTTP/1.1
Content-Type: application/json
Authorization: Bearer {{jwt}}
```
{% endraw %}

Alternatively, the JWT can be manually added to the Authorization header
using the `Bearer <your.jwt.here>` format where the JWT is added to the
request.

### Starting and Stopping the Application

Now that the containers have been created, it is easy to start and stop 
the application.

Open a terminal or command prompt and use the commands to start the
containers:
```
docker start containers-db
docker start containers-api
```

And then to stop them:
```
docker stop containers-api
docker stop containers-db
```

### References

- [Introduction to Docker for Java Developers](https://www.linkedin.com/learning/introduction-to-docker-for-java-developers/zero-to-zero-to-hero)
  is a course on LinkedIn Learning that provides an introduction to
  Docker concepts including containers, images, Dockerfile basics,
  containerization best practices, and Dockerfile alternatives
- [Using containers for development](https://docs.docker.com/language/java/develop/)
  is an overview provided by Docker Docs that gives guidance on how to
  quickly use Docker Compose to create a MySQL container, managed
  volumes, and connect it to the application using a network
