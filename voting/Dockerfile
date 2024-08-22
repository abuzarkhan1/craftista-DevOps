FROM maven:4-eclipse-temurin-19-alpine as build 

WORKDIR /app

COPY . .

RUN mvn package 

FROM openjdk:19-jdk-alpine3.16

WORKDIR /app

COPY --form=build /app/target/voting-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
