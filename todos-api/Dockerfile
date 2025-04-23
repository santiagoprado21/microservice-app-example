# Use an official Node.js runtime as a parent image
FROM node:8.17.0

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./
RUN npm install

# Bundle app source
COPY . .

# Expose the port the app runs on
EXPOSE 8082

# Define environment variable
ENV TODO_API_PORT=8082
ENV JWT_SECRET=PRFT
ENV REDIS_HOST=redis-stack-server
ENV REDIS_PORT=6379
ENV REDIS_CHANNEL=log_channel

# Command to run the application8
CMD ["node", "server.js"]