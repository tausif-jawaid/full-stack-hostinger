# ---------- BUILD STAGE ----------
# Use Node.js version 22 with lightweight Alpine Linux image
# This stage is named "build" so we can use its files later
FROM node:22-alpine AS build

# Set the working directory inside the container
# All next commands will run inside /app
WORKDIR /app

# Copy package.json and package-lock.json files
# We copy this first to install dependencies
COPY package*.json ./

# Install all project dependencies
# Example: React, Vite, Axios etc.
RUN npm install

# Copy all project source files into container
# Example: src, public, configs etc.
COPY . .

# Build the React app for production
# This creates optimized files inside dist folder
RUN npm run build


# ---------- PRODUCTION STAGE ----------
# Start a fresh lightweight container for production
# This keeps final image smaller and cleaner
FROM node:22-alpine

# Set working directory inside production container
WORKDIR /app

# Install "serve" package globally
# This package serves static React build files
RUN npm install -g serve

# Add global npm binaries to system PATH
# So "serve" command works anywhere in container
ENV PATH="/usr/local/bin:$PATH"

# Copy only built files from build stage
# We do not copy source code, only production files
COPY --from=build /app/dist ./dist

# Inform Docker that app runs on port 3000
EXPOSE 3000

# Start the React app when container starts
# -s = single page app mode
# -l = listen on port 3000
CMD ["serve", "-s", "dist", "-l", "3000"]