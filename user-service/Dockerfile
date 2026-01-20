FROM eclipse-temurin:21-jdk-jammy AS builder
WORKDIR /app

COPY gradle gradle
COPY gradlew .
COPY build.gradle .
COPY settings.gradle .
COPY src src

RUN chmod +x gradlew && ./gradlew bootJar -x test --no-daemon

RUN cp /app/build/libs/*.jar /app/user-service.jar

FROM eclipse-temurin:21-jre-jammy
RUN groupadd -r spring && useradd -r -g spring spring
USER spring:spring
WORKDIR /app
COPY --from=builder /app/user-service.jar user-service.jar
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "/app/user-service.jar"]