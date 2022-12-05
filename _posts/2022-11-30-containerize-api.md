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

The Spring Boot application requires three environment variables in
order to make a connection to the MySQL database. Their values are:
  ```
  DB_URL=jdbc:mysql://localhost:3306/containers
  DB_USERNAME=root
  DB_PASSWORD=password
  ```

In three steps, we will create:
- A Docker image of the Spring Boot application using Maven
  (named `containers` with the tag `spring-boot`)
- Two Docker volumes to manage MySQL (`mysql_data` and `mysql_config`),
  which will connect the application's data to local storage
- A Docker network to connect MySQL to the Spring Boot application
  (`mysqlnet`)
- Two Docker containers to run the MySQL and Spring Boot application
  instances (`mysqlserver` and `containers-api`)

### Step 1: Create Spring Boot Image

The pom.xml file includes the image configuration in the `plugins`
section. The Docker username can be updated to the username used to
sign into the Docker application:
  ```
  <plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
      <image>
        <name>containers:spring-boot</name>
      </image>
    </configuration>
  </plugin>
  <plugin>
    <groupId>com.google.cloud.tools</groupId>
    <artifactId>jib-maven-plugin</artifactId>
    <version>3.2.0</version>
    <configuration>
      <to>
        <image>docker.io/docker-username/containers:jib</image>
      </to>
    </configuration>
  </plugin>
  ```
This configuration provides Maven with the container's name and tag,
along with the configuration for
[Google Jib](https://cloud.google.com/blog/products/application-development/introducing-jib-build-java-docker-images-better)
to assist with layering the application to minimize its size.

Then use Maven in the terminal to package the application and build the
image:
  ```
  ./mvnw package -DskipTests spring-boot:build-image
  ```

Execute the command `docker images` to confirm the image exists. The
images for `paketobuildpacks/run` and `pakettobuildpacks/builder`
will appear along with the newly created `containers` image.

#### Breakdown

- `containers:spring-boot` represents the image's name and tag
- `docker.io/docker-username/containers:jib` in the `pom.xml` will need
  to be updated to include a Docker account username and includes
  `containers` as the name of the image being created
- the application is packaged using configuration in the `pom.xml` and
  Maven in the terminal to create a Docker image of the application

### Step 2: MySQL Volumes, Network, and Container

Create Docker volumes:
```
docker volume create mysql_data
docker volume create mysql_config
```

Then create Docker network:
```
docker network create mysqlnet
```

Next, create a container from the MySQL image:
```
docker run -it -d -v mysql_data:/var/lib/mysql -v mysql_config:/etc/mysql/conf.d --network mysqlnet --name mysqlserver -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 mysql
```

This is a good time to initialize the database. The username and password
can be used to sign into MySQL, then the following query can be executed:
```
create database containers;
```

If running the application tests is of interest, there is a schema
located in `sql/schema.sql` that can be run to set up the testing
database. The environment variables to run the tests are almost
identical to the application except the database used it
`containers_test`.

#### Breakdown

- MySQL data is managed using two Docker volumes (`mysql_data` and
  `mysql_config`)
- The application containers will communicate using a Docker network
  (`mysqlnet`)
- The database is managed in the container `mysqlserver` using the
  `mysql` image (provided from Docker Hub), it uses the volumes
  for its data, the `mysqlnet` network for communication on port `3306`,
  and uses the the `root` login with the password `password`

### Step 3: Create Docker Container

Finally, a container is created for the Spring Boot application:
  ```
  docker run -d --name containers-api --network mysqlnet -e DB_URL=jdbc:mysql://mysqlserver:3306/containers -e DB_USERNAME=root -e DB_PASSWORD=password -p 8080:8080 containers:spring-boot
  ```

With both of the containers running, the application will be available
at `http://localhost:8080/api`.

#### Breakdown

- The application container is created with the name `containers-api`
  using the `mysqlnet` network, the environment variables needed to
  make a connection with the database over the network, exposes port
  `8080`, and uses the `containers:spring-boot` container from the
  previous step

### Sending an HTTP Request

An account can be created by sending a request to the application.
The request can be executed using REST Client in VS Code by using the
file `requests.http` containing:
```
@url = http://localhost:8080

POST {{url}}/api/appUsers HTTP/1.1
Content-Type: application/json

{
  "username": "my-username",
  "password": "P@ssw0rd!"
}
```

The same request body can be sent to `http://localhost:8080/authenticate`
to receive a JWT token. Use this token by adding it to the `@jwt`
reference at the top of the `requests.http` file. This will use the  
token to view the users endpoint at `http://localhost:8080/api/appUsers`
with the request:
```
@jwt = <your.jwt.here>

...

GET {{url}}/authenticate HTTP/1.1
Content-Type: application/json
Authorization: Bearer {{jwt}}
```

Alternatively, the JWT can be manually added to the Authorization header
using the `Bearer <your.jwt.here>` format where the JWT is added to the
request.

### References

- [Introduction to Docker for Java Developers](https://www.linkedin.com/learning/introduction-to-docker-for-java-developers/zero-to-zero-to-hero)
  is a course on LinkedIn Learning that provides an introduction to
  Docker concepts including containers, images, Dockerfile basics,
  containerization best practices, and Dockerfile alternatives
- [Using containers for development](https://docs.docker.com/language/java/develop/)
  is an overview provided by Docker Docs that gives guidance on how to
  quickly use Docker Compose to create a MySQL container, managed
  volumes, and connect it to the application using a network
