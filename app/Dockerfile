FROM node:14 AS build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
FROM tauri AS tauri-build
WORKDIR /tauri
COPY --from=build-stage /app/public /tauri/src-tauri/src
RUN tauri build
FROM ubuntu:20.04
WORKDIR /app
COPY --from=tauri-build /tauri/target/release /app
CMD ["./app"]
