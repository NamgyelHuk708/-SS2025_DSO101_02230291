# Basic Docker Containerization

## Introduction
This pratical explains how to containerize a React application using Docker. It covers setting up a Dockerfile, running the application in a container, using Docker Compose, and optimizing with a multi-stage build.

## Basic Docker Containerization

### Step 1: Initialize
Clone the repo and run it locally to ensure that the application is functioning correctly before containerizing it.

### Step 2: Create a Dockerfile on the Root Working Directory
Create a `Dockerfile.test` under the root directory of the React app. The Dockerfile contains instructions on how to build the Docker image for the application.

![alt text](image/step2.png)

### Step 3: Build the Docker Image
Build the Docker image using the following command:

```sh
docker build -f Dockerfile.test -t namgyelhuk708/react-app .
```

This creates a Docker image that contains the application and its dependencies, ready to be run as a container.

![alt text](image/step3.png)

### Step 4: Run the Docker Container
Run the Docker container with port forwarding and volume mounting:

```sh
docker run -d -p 3000:3000 -v /app/node_modules -v $(pwd):/app namgyelhuk708/react-app
```

This starts the application inside a Docker container and makes it accessible on your local machine via `localhost:3000`.

![alt text](image/step4.png)

### Step 5: Verify the Application
Open a web browser and navigate to:

```
http://localhost:3000
```

Check that the container is running using:

```sh
docker ps
```

![alt text](<image/step 5.png>)

![alt text](image/step51.png)

### Step 6: Stop the Container
To stop the running container, first check the container ID:

```sh
docker ps
```

Then stop the container using:

```sh
docker stop [container_id]
```

![alt text](image/step6.png)

### Step 7: Create a `docker-compose.yml` File
Create a `docker-compose.yml` file to define and run multi-container Docker applications. This simplifies running multiple services (e.g., web and test) with a single command.

![alt text](image/step_7.png)

### Step 8: Start the Services with Docker Compose
Start the services defined in `docker-compose.yml` using:

```sh
docker compose up -d --build
```

This runs both the web and test services with a single command.

![alt text](image/step_8.png)

### Step 9: Verify the Services
Check that both the web and test services are running:

```sh
docker ps
```

To interact with a running Docker container using the interactive shell:

```sh
docker exec -it 'web container id' sh
```

Then use:

```sh
npm start
```

To exit the shell, use:

```sh
exit
```

![alt text](image/step9.png)

![alt text](image/step91.png)

### Step 10: Update the `docker-compose.yml`
Make necessary updates to the `docker-compose.yml` file as needed.

![alt text](image/step10.png)

### Step 11: Stop the Services
To stop the running services:

```sh
docker compose stop
```

![alt text](image/step11.png)

## Multi-Step Build Process with Different Base Images

### Step 1: Create a New Dockerfile
Create a new Dockerfile for the multi-step build process.

![alt text](image/step21.png)

### Step 2: Run the Docker Container
Use the following command:

```sh
docker compose up -d --build
```

![alt text](image/step22.png)

### Step 3: Verify the Services
Check the running containers:

```sh
docker ps
```

![alt text](image/step23.png)

### Step 4: Stop the Services
To stop the running services:

```sh
docker compose stop
```

![alt text](image/step24.png)

### Step 5: Remove `Dockerfile.test` and Rebuild
Remove `Dockerfile.test` and run:

```sh
docker build .
```

This will generate an image ID.

![alt text](image/step25.png)

### Step 6: Start the Multi-Phase Container
Use the generated image ID to start the container:

```sh
docker run -d -p 80:80 [image_id]
```

![alt text](image/step26.png)

![alt text](image/step261.png)

## Conclusion
By following these steps, we had successfully containerized a React application using Docker, enabling seamless deployment across different environments.
