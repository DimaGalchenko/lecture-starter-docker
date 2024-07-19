FROM node:20-alpine as build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY public ./public
COPY src ./src
COPY tsconfig*.json ./
COPY vite.config.ts ./
COPY index.html ./
COPY .env.development ./
COPY .env.production ./

RUN npm run build

FROM nginx:1.22.1

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]