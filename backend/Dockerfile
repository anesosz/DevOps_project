# Choose a Java JRE base image
FROM openjdk:17.0.10-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the compiled Java files (bytecode) into the container
COPY Main.class /app

# Run the Java application
CMD ["java", "Main"]


