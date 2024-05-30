# 3-Tier Application Setup

## Overview

This project sets up a 3-tier application architecture using Docker containers consisting of:
1. **Database**: PostgreSQL
2. **Backend**: JavaAPI
3. **Frontend**: Apache HTTP Server 

`Ansible`, `SonarCloud`, and `GitHub Actions` are integrated to automate various tasks and streamline the CI/CD pipeline. For detailed information on each integration, please refer to the `README` of each component.

## Instructions

**To build and run the entire application, follow these steps:**

1. Navigate to the root directory of the project where the docker-compose.yml file is located.
2. Run the following command to start and run all the services defined in docker-compose.yml: 
```bash
docker-compose up --build
```
This command will build the Docker images for each service and start containers for the database, backend, and frontend.

Once all services are up and running, you can access the application via localhost:80 in your web browser. 
Refer to the `README` files for each component `(Database, Backend, Frontend)` for more information on how to interact with them.


**To stop and remove the containers, networks, and volumes defined in docker-compose.yml, use the following command:**
```bash
docker-compose down
```

## Note
Ensure that you have Docker installed and running on your system before proceeding with the above steps. Additionally, make sure to follow any specific instructions provided in the README files for each component to configure and set up the application properly.