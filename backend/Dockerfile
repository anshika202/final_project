# Step 1: Build using Maven
FROM maven:3.9.6-eclipse-temurin-17 AS builder

WORKDIR /app

# Copy everything to the container
COPY . .

# Build the app (produces target/*.jar)
RUN mvn clean package -DskipTests

# Step 2: Run the app using OpenJDK
FROM openjdk:17-jdk-slim

WORKDIR /app

# Copy built JAR from builder stage
COPY --from=builder /app/target/*.jar app.jar

# Expose the app port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
