# Use an official Maven 3.9.6 image with OpenJDK 17 to build the application
FROM maven:3.9.6-openjdk-17-slim AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the pom.xml and the source code into the container
COPY pom.xml .
COPY src ./src

# Build the application (this will create a .jar file)
RUN mvn clean package -DskipTests

# Use a smaller openjdk 17 image for running the app
FROM openjdk:17-jre-slim

# Set the working directory
WORKDIR /app

# Copy the built .jar file from the build image
COPY --from=build /app/target/demo-0.0.1-SNAPSHOT.jar demo.jar

# Set the command to run the Java application
ENTRYPOINT ["java", "-jar", "demo.jar"]
