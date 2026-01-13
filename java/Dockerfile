# ============================================================
# HSL InfoDevOps Base Image for Java Microservices (runtime-only)
# Built for AKS — optimized, secure, slim
# ============================================================

# =====================
# Test stage
# =====================
FROM eclipse-temurin:25-jdk-jammy

WORKDIR /app
COPY pom.xml .
RUN mvn -B -q dependency:go-offline

COPY src ./src
RUN mvn test

# =====================
# Build stage
# =====================
FROM eclipse-temurin:25-jdk-jammy AS build
WORKDIR /app
COPY . .
RUN mvn package -DskipTests

# =====================
# Runtime stage
# =====================
FROM eclipse-temurin:25-jre-jammy
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

ENV JAVA_TOOL_OPTIONS="-XX:+UseContainerSupport -XX:MaxRAMPercentage=75"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
    && rm -rf /var/lib/apt/lists/*

CMD ["java", "-version"]
