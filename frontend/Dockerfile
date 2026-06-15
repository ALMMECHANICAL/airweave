FROM node:26.3.0-slim@sha256:95a34da32a840bd9b3b09a5b773591c16923e350174b1c50e1200c75bf15eaa9 AS builder

WORKDIR /app

# Copy package files
COPY package.json ./

# First install dependencies without using the lockfile
# Skip postinstall scripts to avoid @swc/core segfault
RUN npm install --no-package-lock --ignore-scripts

# Copy application code
COPY . .

# Build the application in production mode
# Increase Node memory and use npx to run vite directly
RUN NODE_OPTIONS="--max-old-space-size=4096" npx vite build

# Runtime stage
FROM node:26.3.0-alpine@sha256:3ad34ca6292aec4a91d8ddeb9229e29d9c2f689efd0dd242860889ac71842eba

WORKDIR /app

RUN apk upgrade --no-cache

# Install serve for hosting the built app
RUN npm install -g serve

# Copy built app from builder stage
COPY --from=builder /app/dist /app/dist
COPY docker-entrypoint.sh /usr/local/bin/
COPY serve.json /app/serve.json

# Make entrypoint executable
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

# Use entrypoint script for runtime configuration
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
