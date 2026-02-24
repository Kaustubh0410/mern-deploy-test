# Build stage
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build --configuration production

# Serve stage
FROM nginx:alpine
# Copy the build output to replace the default nginx contents.
# The output folder name in angular.json is "dist/angular-15-crud"
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
