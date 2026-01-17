# ============================================================
# HSL InfoDevOps Base Image for Java Microservices (runtime-only)
# Built for AKS — optimized, secure, slim
# ============================================================

FROM eclipse-temurin:25-jre-jammy

WORKDIR /app

ENV JAVA_TOOL_OPTIONS="-XX:+UseContainerSupport -XX:MaxRAMPercentage=75"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
    && rm -rf /var/lib/apt/lists/*

CMD ["java", "-version"]
