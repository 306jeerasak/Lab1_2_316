FROM node:20-alpine AS build
WORKDIR /app

# copy full project first (so Quasar folder structure is present)
COPY . .

# prevent postinstall from running (quasar prepare) during image build
ENV npm_config_ignore_scripts=true

RUN npm install

# now run quasar build (this does not rely on postinstall)
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist/spa /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
