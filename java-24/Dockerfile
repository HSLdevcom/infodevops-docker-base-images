# ============================================================
# HSL InfoDevOps Base Image for Java Microservices (runtime-only)
# Built for AKS — optimized, secure, slim
# ============================================================

FROM eclipse-temurin:24-jre-jammy

# Set default workdir
WORKDIR /app

# Set important env vars for JVM in containers
ENV JAVA_TOOL_OPTIONS="-XX:+UseContainerSupport -XX:MaxRAMPercentage=75"

# Install common debugging tools (optional)
RUN apt-get update && apt-get install -y curl && apt-get clean

# Default CMD (overwritten by service images)
CMD ["java", "-version"]
