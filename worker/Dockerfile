FROM maven AS builder

WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src

RUN mvn clean package 

FROM openjdk:8-jre-slim

WORKDIR /app

COPY --from=builder /app/target/worker-jar-with-dependencies.jar worker.jar

CMD ["java", "-jar", "worker.jar"]