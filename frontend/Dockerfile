# Frontend Dockerfile
FROM node:18-alpine AS build
WORKDIR /app
COPY frontend/package.json ./
COPY frontend/package-lock.json* ./
RUN npm ci --silent || npm install
COPY frontend/ ./frontend/
WORKDIR /app/frontend
RUN npm run build

FROM nginx:stable-alpine
COPY --from=build /app/frontend/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
