# Stage 1: Build React frontend
FROM node:18 as build

WORKDIR /app

# Install npm dependencies
COPY package*.json ./
RUN npm install 

# Copy the rest of the application files
COPY . .

# Build the React application
RUN npm run build

# Stage 2: Serve React frontend with nginx
FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
