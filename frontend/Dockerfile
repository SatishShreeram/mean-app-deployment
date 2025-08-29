# Use an official Node.js image to build the Angular app
FROM node:18-alpine as build

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the application source code
COPY . .

# Build the Angular application
RUN npm run build -- --output-path=./dist/

# Use a lightweight Nginx image to serve the built application
FROM nginx:alpine as final

# Copy the built application from the 'build' stage to the Nginx serving directory
COPY --from=build /app/dist/frontend-task-mean-app /usr/share/nginx/html

# Expose port 80 for Nginx
EXPOSE 80

# Command to start Nginx (this is the default for the nginx:alpine image)
CMD ["nginx", "-g", "daemon off;"]