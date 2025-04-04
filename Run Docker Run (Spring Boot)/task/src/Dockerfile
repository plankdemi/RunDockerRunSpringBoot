# ----------- Build stage -----------
FROM eclipse-temurin:21-jdk AS builder

WORKDIR /app

# Copy Gradle Wrapper scripts
COPY gradlew gradlew.bat ./

# Copy Gradle wrapper config
COPY gradle/wrapper ./gradle/wrapper

# Copy Gradle build files
COPY build.gradle settings.gradle ./

# Copy application source code
COPY src/ ./src/

# Make Gradle wrapper executable
RUN chmod +x ./gradlew

# Build the application
RUN ./gradlew bootJar --no-daemon


# ----------- Package stage -----------
FROM eclipse-temurin:21-jre AS runtime

WORKDIR /app

# Copy the jar from the builder stage and rename it to app.jar
COPY --from=builder /app/build/libs/hyper-web-app-0.0.1-SNAPSHOT.jar app.jar

# Expose default Spring Boot port
EXPOSE 8080

# Set entry point to run the app
ENTRYPOINT ["java", "-jar", "app.jar"]
