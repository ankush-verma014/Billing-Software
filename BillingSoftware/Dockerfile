# ✅ Render + Alpine FIXED version
FROM eclipse-temurin:17-jdk-alpine AS builder
WORKDIR /app

# Install Maven (Alpine mein nahi hota)
RUN apk add --no-cache maven

COPY pom.xml .
RUN mvn dependency:go-offline -B
COPY src ./src
RUN mvn clean package -DskipTests

# Production stage
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE $PORT
ENTRYPOINT ["java", "-jar", "app.jar"]




