# ============================================================
# HSL InfoDevOps Base Image for node.js Microservices (runtime-only)
# Built for AKS — optimized, secure, slim
# ============================================================

FROM node:22-slim AS base

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    tini \
  && rm -rf /var/lib/apt/lists/*

USER node
RUN mkdir -p /home/node/app
WORKDIR /home/node/app

FROM base AS installer
ENV NODE_ENV=development
COPY --chown=node:node package*.json ./
RUN npm ci

FROM base AS node_modules
ENV NODE_ENV=production
COPY --chown=node:node package*.json ./
RUN npm ci --omit=dev

FROM installer AS builder
ENV NODE_ENV=production
COPY --chown=node:node . .
RUN npm run build

FROM node:22-slim AS standardized_image

ARG DEBIAN_FRONTEND=noninteractive
ENV NODE_ENV=production

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    tini \
  && rm -rf /var/lib/apt/lists/*

USER node
RUN mkdir -p /home/node/app
WORKDIR /home/node/app

COPY --from=builder --chown=node:node /home/node/app/dist ./dist
COPY --from=node_modules --chown=node:node /home/node/app/node_modules ./node_modules

ENTRYPOINT ["/usr/bin/tini", "--"]

CMD ["node", "./dist/index.js"]
