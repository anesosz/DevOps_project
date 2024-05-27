# Database Setup

## Steps to Build and Run the PostgreSQL Container

1. **Build the Docker Image:**
    ```bash
    docker build -t postgres:14.1-alpin .
    ```

2. **Create the Network:**
    ```bash
    docker network create app-network
    ```

3. **Run the PostgreSQL Container:**
    ```bash
    docker run --name MypostgresSQL -p 5432:5432 --net=app-network -e POSTGRES_PASSWORD=pwd -d postgres:14.1-alpine
    ```

4. **Verify the Database:**
    ```bash
    docker exec -it MypostgresSQL psql -U usr -d db
    ```

5. **Restart Adminer (optional):**
    ```bash
    docker run -p "8090:8080" --net=app-network --name=adminer -d adminer
    ```

## Initialization SQL Script

The `CreateScheme.sql` and `InsertData.sql` are executed in alphabetical order when the container starts up.

## Answers for questions

**Does it seem right to have passwords written in plain text in a file?**
 No, storing passwords in plain text files is not secure. Passwords should be securely hashed or encrypted to protect them from unauthorized access.

**Why should we run the container with a flag -e to give the environment variables?**
Running the container with the -e flag allows you to provide environment variables to configure the container at runtime. This is useful for passing sensitive information like passwords securely without exposing them in the Dockerfile or command-line history.

**Why do we need a volume to be attached to our postgres container?**
Attaching a volume to a PostgreSQL container allows you to persist data outside of the container's filesystem. This is important for ensuring that data is not lost when the container is stopped or removed. Volumes also facilitate data sharing between containers and can be used for backups and migrations.