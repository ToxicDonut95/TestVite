# Stage 1: Build the React app
FROM node:21 AS builder

WORKDIR /app

# Copy package.json and yarn.lock to install dependencies
COPY package.json .

# Install dependencies
RUN yarn install

# Copy the entire application code to the container
COPY . .

# Build the React app
RUN yarn run build

# Stage 2: Serve the built app using Nginx
FROM nginx:alpine

# Copy the built React app from the builder stage to Nginx's web server directory
COPY --from=builder /app/ /usr/share/nginx/html/

# Copy custom nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80 (Note: This is only for documentation purposes)
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]