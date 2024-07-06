# Stage 1: Build React frontend
FROM node:14 as build

WORKDIR /app

# Clear npm cache
RUN npm cache clean --force

# Set npm configuration to use HTTPS for Git
RUN npm config set git-protocol https

# Set npm proxy configuration if needed
# RUN npm config set proxy http://your-proxy-url:port
# RUN npm config set https-proxy http://your-proxy-url:port

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

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
