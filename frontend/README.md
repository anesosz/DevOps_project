# Frontend (HTTP Server) Setup

## Steps to Build and Run the Frontend Server Container

1. **Build the Docker Image:**
    ```bash
    docker build -t my-frontend-server .
    ```

2. **Run the Frontend Server Container:**
    ```bash
    docker run --name my-frontend-server-container -p 80:80 --net=app-network -d my-frontend-server
    ```

3. **Verify the Frontend:**
    Visit `http://localhost` in your web browser. You should see the HTML page with the message "Welcome to the 3-Tier Application".
