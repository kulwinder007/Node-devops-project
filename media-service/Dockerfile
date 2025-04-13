# Use the official Node.js 18 image with Alpine Linux as the base image
FROM node:18-alpine

# Install Redis and RabbitMQ dependencies
RUN apk update && apk add --no-cache \
  redis \
  rabbitmq-server \
  bash

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy the package.json and package-lock.json (if exists)
COPY package*.json ./

# Install the Node.js dependencies
RUN npm ci --only=production

# Copy the rest of the application code
COPY . .

# Expose necessary ports (for media service and Redis/RabbitMQ)
EXPOSE 4006
# Redis default port
EXPOSE 6379   
 # RabbitMQ default port
 EXPOSE 5672  

# Start Redis, RabbitMQ, and the Node.js application
CMD redis-server --daemonize yes && \
    rabbitmq-server -detached && \
    node src/server.js
