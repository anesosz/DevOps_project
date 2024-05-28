# Frontend (HTTP Server) Setup

## Steps to Build and Run the Frontend Server Container

1. **Build the Docker Image:**
    ```bash
    docker build -t httpd:2.4 .
    ```

2. **Run the Frontend Server Container:**
    ```bash
    docker run -d -p 80:80 --name Myhttpd --net=app-network httpd:2.4
    ```

3. **Verify the Frontend:**
    Visit `http://localhost` in your web browser. You should see the HTML page with the message "Welcome to the My Application!".


## Answers for questions
**Why do we need a reverse proxy?**
A reverse proxy is needed to distribute client requests to multiple backend servers, enhance security by masking the identity of backend servers, improve load balancing, and provide caching and SSL termination.

**Why is docker-compose so important?**
Docker Compose is important because it simplifies the management and orchestration of multi-container Docker applications, allowing developers to define and run complex applications using a simple YAML file. It ensures consistency across environments and facilitates easy scaling, networking, and service dependencies.

**Why do we put our images into an online repo?**
We put our Docker images into an online repository to ensure easy sharing, versioning, and deployment of application containers across different environments. This facilitates collaboration, continuous integration/continuous deployment (CI/CD) workflows, and provides a centralized place to store and access container images.
