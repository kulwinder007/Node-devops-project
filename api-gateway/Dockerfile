# Use the official node.js 18 image with Alpine Linux as the base image
FROM node:18-alpine

# Set the working directory in the container
WORKDIR /usr/src/app

# Install Redis inside the container
RUN apk update && apk add --no-cache redis

# Install Node.js dependencies
COPY package*.json ./
RUN npm ci --only=production

# Copy the rest of the application code
COPY . .

# Expose the port for the API Gateway
EXPOSE 4000
#Expose Redis port
EXPOSE 6379

# Start Redis and the API Gateway (Node.js server)
CMD redis-server --daemonize yes && node src/server.js
