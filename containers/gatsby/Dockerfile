TODO: Fix this file. (this comment will intentionally break the file, because it needs editing)

# This is a multi-stage build process that builds the React SPA
# and copies the production output into an nginx image. That nginx
# server runs on port 3000, which is upstream of port 80 on the main
# user-facing nginx server.
FROM node:12-alpine as builder
WORKDIR "/app"
COPY ./package.json ./
RUN npm install
# RUN gatsby telemetry --disable
COPY . .
RUN npm run build

FROM nginx
EXPOSE 8000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
