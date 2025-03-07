# build stage
FROM node:12-alpine as build-stage
RUN apk add --no-cache git
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# production stage
FROM node:18-alpine as production-stage
WORKDIR /app
RUN npm install -g serve
COPY --from=build-stage /app/dist /app
EXPOSE 8087
CMD ["serve", "-s", ".", "-l", "8087", "--no-clipboard", "--host", "0.0.0.0"]
