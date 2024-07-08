# Stage 1: Build React frontend
FROM node:18 as build

WORKDIR /app

# Install npm dependencies
COPY package.json package-lock.json ./

# install the dependencies
RUN npm install

# Update npm to the latest version
RUN npm install -g npm@latest

# Copy the rest of the application files
COPY . .

# Build the React application
RUN npm run build

# Stage 2: Serve React frontend with nginx
FROM nginx:alpine

# Copy built files from the build stage
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
