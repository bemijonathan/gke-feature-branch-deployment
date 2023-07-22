# Use an official Node runtime as a base image
FROM --platform=linux/amd64 node:16 as build

# Set the working directory in the container to /app
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install the application dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Build the app for production
RUN npm run build

# Use Nginx to serve the static files
FROM nginx:1.21.1

# Copy the build output from the first stage build
COPY --from=build /app/build /usr/share/nginx/html

# Expose the port Nginx is running on
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
