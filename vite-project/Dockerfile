# Stage 1: Build React application
FROM node:14 as build

# Set working directory
WORKDIR /app

# Copy package.json and yarn.lock
COPY package.json yarn.lock ./

# Set custom network timeout for yarn install
ENV npm_config_network_timeout=600000

# Install dependencies
RUN yarn install --frozen-lockfile

# Copy the rest of the application code
COPY . .

# Build the React application
RUN yarn build


# Stage 2: Setup NGINX server to serve built React app
FROM nginx:latest

# Copy built React application from the previous stage
COPY --from=build /app/build /usr/share/nginx/html

# Optionally, remove the default NGINX configuration file
RUN rm -rf /etc/nginx/conf.d/default.conf

# Optionally, copy your NGINX configuration file (if needed)
COPY nginx.conf /etc/nginx/conf.d/

# Expose port 80 (default HTTP port)
EXPOSE 80

# Start NGINX server in the foreground
CMD ["nginx", "-g", "daemon off;"]
