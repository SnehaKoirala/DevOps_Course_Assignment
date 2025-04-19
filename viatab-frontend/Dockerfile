# Step 1: Use Node.js image to build the app
FROM node:16 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json for better caching
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the app's source code
COPY . .

# Build the React app
RUN npm run build

# Step 2: Serve the React app using an Nginx server
FROM nginx:alpine

# Copy the build files from the previous image to Nginx's public directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose the port Nginx is serving the app
EXPOSE 80

# Start the Nginx server to serve the app
CMD ["nginx", "-g", "daemon off;"]
