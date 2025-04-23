# Use an official Maven image as the base image
FROM openjdk:8-jdk-alpine AS build
# Set the working directory in the container
COPY . /app
WORKDIR /app
# Copy the pom.xml and the project files to the container
# Build the application using Maven
RUN ./mvnw clean package -DskipTests
# Copy the built JAR file from the previous stage to the container

FROM openjdk:8-jre-alpine
# Set the working directory in the container
WORKDIR /app
# Copy the built JAR file from the previous stage to the container
COPY --from=build /app/target/users-api-0.0.1-SNAPSHOT.jar ./my-application.jar

ENV JWT_SECRET=PRFT
ENV SERVER_PORT=8083

# Set the command to run the application
CMD ["java", "-jar", "my-application.jar"]