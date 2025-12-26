# 🔥 Java 21 + Alpine (Render Perfect)
FROM eclipse-temurin:21-jdk-alpine AS builder
WORKDIR /app

# Maven install (Alpine)
RUN apk add --no-cache maven

COPY pom.xml .
RUN mvn dependency:go-offline -B
COPY src ./src
RUN mvn clean package -DskipTests

# Production (Java 21 JRE)
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE $PORT
ENTRYPOINT ["java", "-jar", "app.jar"]
