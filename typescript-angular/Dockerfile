# Stage 1
FROM node:14 as build

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

# depends on your package.json script
RUN npm run build-prod

# Stage 2
FROM nginx:alpine

# depends on your src/environment/*.ts build path
COPY --from=build /app/dist/Prod-SatuFramework /usr/share/nginx/html

COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]