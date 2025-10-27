# When you use multi-stage builds in Docker, each FROM statement starts a new, clean image layer.

# Stage 1
FROM node:22-alpine AS build-stage

WORKDIR /frontend-app
COPY package.json ./
COPY public public
COPY src src

RUN npm install
RUN npm run build

# EXPOSE 3000
# CMD [ "npm", "start" ]

# Stage 2
FROM nginx:alpine-slim
# Copy files from first stage
# COPY --from=0 /usr/share/nginx/html
COPY --from=build-stage /frontend-app/build /usr/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]
