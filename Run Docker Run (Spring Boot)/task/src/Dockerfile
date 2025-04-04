#build stage
FROM amazoncorretto AS builder


WORKDIR /app

COPY graddlew gradlew.bat ./gradle/
COPY build.gradle settings.gradle ./

RUN chmod a+x ./gradlew
COPY ../src/ ./src/

RUN ./gradlew bootJar --no-daemon


#run stage
FROM eclipse-temurin:21-jre
WORKDIR /app
COPY --from=builder ./app.jar .

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
