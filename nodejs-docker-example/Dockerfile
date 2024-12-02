# Stage 1: Build Stage
FROM node:18 AS builder

# Set the working directory
WORKDIR /build

# Copy package files and install dependencies (including devDependencies)
COPY package*.json ./
RUN npm install

# Copy the application source code and build it
COPY tsconfig.json ./
COPY src/ ./src/
RUN npm run build

# Stage 2: Runtime Stage
FROM node:18 AS runner

# Set the working directory
WORKDIR /app

# Copy only the necessary runtime files from the build stage
COPY --from=builder /build/package*.json ./
COPY --from=builder /build/node_modules ./node_modules/
COPY --from=builder /build/dist ./dist/

# Expose the application port (optional)
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]
