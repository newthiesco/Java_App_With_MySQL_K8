# Stage 1: Build the Java application
FROM techiescamp/jdk-17:1.0.0 AS build

WORKDIR /app

# Copy only the necessary files for Maven to resolve dependencies
COPY pom.xml /app/
# Run Maven in one step to cache dependencies and build the app
COPY src /app/src/
RUN mvn clean install -DskipTests

# Stage 2: Create a smaller runtime image
FROM techiescamp/jre-17:1.0.0

WORKDIR /app

# Copy the JAR file from the build stage
COPY --from=build /app/target/*.jar ./java.jar

# Expose the port the app runs on
EXPOSE 8080

# Run the jar file
CMD ["java", "-jar", "java.jar"]

