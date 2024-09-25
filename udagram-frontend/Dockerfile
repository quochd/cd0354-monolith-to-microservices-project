FROM node:16 AS build

# Install Ionic CLI globally
RUN npm install -g @ionic/cli

# Set working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json files
COPY package*.json ./

# Install app dependencies
RUN npm ci --legacy-peer-deps

# Copy the rest of the application
COPY . .

# Build the application
RUN npx ionic build

### Production Stage ###
FROM nginx:alpine

# Copy built files from the previous stage
COPY --from=build /usr/src/app/www /usr/share/nginx/html