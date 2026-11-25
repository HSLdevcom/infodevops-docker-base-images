# syntax=docker/dockerfile:1
# check=error=true

# ============================================================
# HSL InfoDevOps Base Image for Java Microservices (Java Development Kit)
# Built for AKS — optimized, secure, slim
# ============================================================

# Pinned to a patched Temurin release (CVE-2026-114938 "Java4Shell" is fixed in 25.0.5.1).
FROM eclipse-temurin:25.0.5.1_2-jdk-jammy

WORKDIR /app

ENV JAVA_TOOL_OPTIONS="-XX:+UseContainerSupport -XX:MaxRAMPercentage=75"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
    && rm -rf /var/lib/apt/lists/*

CMD ["java", "-version"]
