# Use official Node.js 22 lightweight Alpine image as base
FROM node:22-alpine

# Set working directory inside container
WORKDIR /app

# Copy package files first for dependency installation
COPY package*.json ./

# Install all Node.js dependencies
RUN npm install

# Copy remaining project files into container
COPY . .

# Tell Docker app runs on port 4000
EXPOSE 4000

# Start the application when container starts
CMD [ "npm", "start" ]