# GitHub Actions Workflow Documentation

This directory contains the GitHub Actions workflows used for Continuous Integration (CI) of the project.

## Workflow: CI DevOps 2024

This workflow is designed to automate the build and test process for the backend application in this repository. It ensures that the code is built and tested on every push to the `master` branch and on pull requests.

### Workflow File: `main.yml`

The workflow file is located at `.github/workflows/main.yml`.

### Triggering Events

- **Push to `master` branch:** The workflow is triggered whenever there is a push to the `master` branch.
- **Pull Requests:** The workflow is triggered on pull requests targeting the `master` branch.

### Jobs

#### Job: `test-backend`

This job runs on an Ubuntu 22.04 runner and includes the following steps:

1. **Checkout Code**
    - Uses the `actions/checkout@v3` action to check out the repository code.

2. **Set up JDK 17**
    - Uses the `actions/setup-java@v3` action to set up JDK 17 with the `temurin` distribution.

3. **Build and Test with Maven**
    - Runs the `mvn clean verify` command to build the application and run tests.

### Directory Structure

The `pom.xml` file for the Maven project is located in `backend/simpleapi`. The workflow specifies this directory as the working directory for Maven commands.

# Continuous Delivery (CD) Configuration Documentation

This part consist on the GitHub Actions workflows used for Continuous Delivery (CD) of the project.

## Docker Image Build and Publish Workflow

The primary goal of this workflow is to build Docker images containing our application and publish them to Docker Hub every time there is a commit on the `master` branch.

### 1. Adding Docker Hub Credentials to Environment Variables

We store Docker Hub credentials as secured environment variables in GitHub Actions. These variables are securely accessed within the workflow.

### 2. Building Docker Images

The workflow defines a job `build-and-push-docker-image` that runs on an Ubuntu 22.04 runner. It includes the following steps:

- **Checkout Code:** Uses `actions/checkout@v3` to check out the repository code.
- **Build and Push Backend:** Uses `docker/build-push-action@v3` to build and push the backend Docker image to Docker Hub. The image is tagged with the latest version.

### 3. Publishing Docker Images

The Docker images are published to Docker Hub only when there is a commit on the `master` branch. Before publishing, the workflow logs in to Docker Hub using the secured credentials stored as secrets.

### SonarCloud Quality Gate

SonarCloud is integrated into the workflow to analyze the code quality and enforce best practices. The SonarCloud analysis is triggered on every commit to the `master` branch.

### Setting up Quality Gate

To set up the Quality Gate, you need to:

1. Register for a SonarCloud account and create an organization.
2. Keep track of the project key and organization key.
3. Modify the Maven command in the workflow to include SonarCloud analysis with the correct project and organization keys.

### Bonus: Split Pipelines

If desired, you can separate the jobs into different workflows to ensure:

- The `test-backend` job runs on both `develop` and `main` branches.
- The `build-and-push-docker-image` job runs only on the `main` branch.
- The Docker API image is pushed only if the `test-backend` job is successful.

## References

- [GitHub Actions](https://github.com/features/actions)
- [Docker Hub](https://hub.docker.com/)
- [SonarCloud](https://sonarcloud.io/)
