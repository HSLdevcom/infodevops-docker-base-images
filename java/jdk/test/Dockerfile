# syntax=docker/dockerfile:1
# check=error=true

FROM 25-java-jdk-test:latest

# Fail the build if the image runs a JDK affected by CVE-2026-114938 ("Java4Shell", fixed in 25.0.5.1).
ARG MIN_JAVA_VERSION=25.0.5.1
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN v="$(java -XshowSettings:properties -version 2>&1 | sed -n 's/^ *java\.runtime\.version = //p' | cut -d+ -f1)" \
    && echo "Java runtime version: $v (minimum $MIN_JAVA_VERSION)" \
    && [ "$(printf '%s\n' "$MIN_JAVA_VERSION" "$v" | sort -V | head -n1)" = "$MIN_JAVA_VERSION" ]

CMD ["echo", "hello"]
