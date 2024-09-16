FROM maven:3.8.4-openjdk-11 AS build
WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn clean package -DskipTests


FROM openjdk:11-jdk-slim
WORKDIR /app

COPY --from=build /app/target/payment-service.jar /app/app.jar

EXPOSE 8083

ENTRYPOINT ["java", "-jar", "/app/app.jar"]
