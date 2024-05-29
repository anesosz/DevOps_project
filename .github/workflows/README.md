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