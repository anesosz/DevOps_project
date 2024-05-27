# Building and Running a Simplistic API with Docker

## Overview

This guide demonstrates the process of building and running a simplistic API using Docker containers. We'll cover the convenience of using containers, the importance of multistage builds, and how to access a database container from your backend application.

### 1. How convenient would it be to have a virtual container to build and run our simplistic API?

Using a virtual container to build and run the API would be highly convenient. It ensures consistent behavior, simplifies deployment, and enhances collaboration among team members.

### 2. Why do we need a multistage build? And explain each step of this Dockerfile

Multistage builds are used to create more efficient Docker images by separating the build and run stages into different sections. This helps to reduce the final image size and improve security by including only the necessary artifacts in the final image.

Here's a breakdown of the Dockerfile provided:

- **Build stage (`myapp-build`):**
  - Use the Maven image (`maven:3.8.6-amazoncorretto-17`) as the base image.
  - Set environment variables and working directory.
  - Copy the Maven configuration file (`pom.xml`) and source code into the container.
  - Build the application using Maven, skipping tests.

- **Run stage:**
  - Use the Amazon Corretto JDK image (`amazoncorretto:17`) as the base image.
  - Set environment variables and working directory.
  - Copy the built JAR file from the build stage into the container.
  - Define the entry point to run the Java application.

### 3. How to access the database container from your backend application?

To access the database container from your backend application:

- Ensure both containers are on the same Docker network.
- Use the database container name as the host in your application's database connection configuration.
- Configure the database connection parameters such as URL, username, and password accordingly.

### 4. Running Adminer Container

To run the Adminer container for database management, use the following command:

```bash
docker run -p "8090:8080" --net=app-network --name=adminer -d adminer
```
### 5.Compiling Java Source Code and Building Docker Image

- Compile the Java source code:
    ```bash
    javac Main.java
    ```
- Build the Docker image with JDK 17:
    ```bash
    docker build -t myjava:17 .
    ```

### Steps to Build and Run the API:

1. Build the PostgreSQL Docker image:
   ```bash
   docker build -t postgres:14.1-alpine .
    ```
2. Run the PostgreSQL container:
    ```bash
   docker run --name MypostgresSQL -p 5432:5432 --net=app-network -e POSTGRES_PASSWORD=pwd -d postgres:14.1-alpine
    ```
3. Build the Java application Docker image:
    ```bash
    docker build -t my-java-app .
    ```
4. Run the Java application container:
   ```bash
   docker run --name Myappjava -d --net=app-network -p 8080:8080 my-java-app
    ```




















**1.1 How convenient would it be to have a virtual container to build and run our simplistic API?**
Using a virtual container to build and run the API would be highly convenient. It ensures consistent behavior, simplifies deployment, and enhances collaboration among team members.

**1.2 Why do we need a multistage build? And explain each step of this dockerfile**
Multistage builds are used to create more efficient Docker images by separating the build and run stages into different sections. This helps to reduce the final image size and improve security by including only the necessary artifacts in the final image.

**How to access the database container from your backend application?**
- Ensure Containers are on the Same Network
- Use the Database Container Name as the Host
- Configure Database Connection Parameters
- 

docker build -t  postgres:14.1-alpine .
docker run --name MypostgresSQL -p 5432:5432 --net=app-network -e POSTGRES_PASSWORD=pwd -d postgres:14.1-alpine

javac Main.java
docker build -t myjava:17 .
docker build -t myjava:11-jre-slim .

docker build -t my-java-app .
docker run --name Myappjava -d --net=app-network my-java-app 

# Build stage
FROM maven:3.8.6-amazoncorretto-17 AS myapp-build

# Set environment variable for the application home directory
ENV MYAPP_HOME /opt/myapp

# Set the working directory
WORKDIR $MYAPP_HOME

# Copy the Maven configuration file to the working directory
COPY pom.xml .

# Copy the source code to the working directory
COPY src ./src

# Build the application and skip the tests
RUN mvn package -DskipTests

# Run stage
FROM amazoncorretto:17

# Set environment variable for the application home directory
ENV MYAPP_HOME /opt/myapp

# Set the working directory
WORKDIR $MYAPP_HOME

# Copy the JAR file from the build stage to the working directory
COPY --from=myapp-build $MYAPP_HOME/target/*.jar $MYAPP_HOME/myapp.jar

# Define the entry point for the container
ENTRYPOINT java -jar myapp.jar

