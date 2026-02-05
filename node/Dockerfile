# syntax=docker/dockerfile:1
# check=error=true

# ============================================================
# HSL InfoDevOps Base Image for node.js Microservices (runtime-only)
# Built for AKS — optimized, secure, slim
# ============================================================

FROM node:22-slim AS base

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    ca-certificates \
    tini \
  && rm -rf /var/lib/apt/lists/*

CMD ["node", "--version"]