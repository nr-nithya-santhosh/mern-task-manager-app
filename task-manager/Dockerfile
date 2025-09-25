# client/Dockerfile
# Stage 1: Build the React app
FROM node:18-alpine as build

# This ARG will receive the value from the docker build command
ARG REACT_APP_API_URL

WORKDIR /app

# Set the environment variable for the build
ENV REACT_APP_API_URL=$REACT_APP_API_URL

COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve the app with Nginx
FROM nginx:stable-alpine
# Copy the built files from the 'build' stage to Nginx's public folder
COPY --from=build /app/build /usr/share/nginx/html
# Expose port 80 for the Nginx server
EXPOSE 80
# Command to start Nginx
CMD ["nginx", "-g", "daemon off;"]