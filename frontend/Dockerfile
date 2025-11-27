# Stage 1: build frontend
FROM node:18-alpine AS build
WORKDIR /app

# ติดตั้ง dependencies
COPY package*.json ./
RUN npm install

# คัดลอก source code
COPY . .

# build frontend
RUN npm run build

# Debug: ตรวจสอบว่ามี dist
RUN echo "=== Content of /app ===" && ls -la /app
RUN echo "=== Content of /app/dist ===" && ls -la /app/dist

# Stage 2: serve with nginx
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
