# Step 1: Build stage (Node.js for React/Vite)
FROM node:18 AS build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Step 2: Runtime stage (Tomcat for serving)
FROM nginx:stable-alpine AS production-stage

# Remove default nginx static files and copy our build
RUN rm -rf /usr/share/nginx/html/*

# Copy nginx config and built files from build stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
