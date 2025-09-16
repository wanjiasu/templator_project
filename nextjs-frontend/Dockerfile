FROM node:20-bookworm

# Set the working directory
WORKDIR /app

# Use Corepack to manage pnpm (Node 20 includes Corepack)
RUN corepack enable && corepack prepare pnpm@10.7.1 --activate

# Copy package files and install dependencies (use lockfile for deterministic builds)
COPY package.json pnpm-lock.yaml ./

# Install dependencies using pnpm via Corepack
RUN pnpm install --frozen-lockfile

## Switch to the non-root user
USER node

# Copy the rest of your application code
COPY . .

EXPOSE 3000

# Start the application
CMD ["./start.sh"]