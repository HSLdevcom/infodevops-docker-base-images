# ============================================================
# HSL InfoDevOps Base Image for node.js Microservices (runtime-only)
# Built for AKS — optimized, secure, slim
# ============================================================

# ============================
# Test stage
# ============================
FROM node:22-slim AS test

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci

COPY . .

RUN npm test

# ============================
# Runtime stage
# ============================
FROM node:22-slim AS runtime

ARG DEBIAN_FRONTEND=noninteractive

WORKDIR /app

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    ca-certificates \
    tini \
  && rm -rf /var/lib/apt/lists/*

COPY --from=test /app/node_modules ./node_modules
COPY --from=test /app .

CMD ["node", "--version"]




