FROM jelastic/nodejs:10.16.3-forever as builder

ARG appname
ENV APP_NAME $appname

WORKDIR /${APP_NAME}

COPY package.json package-lock.json ./
# install deps
RUN npm set strict-ssl false
RUN npm install

# build
COPY . ./
# RUN npm run build

FROM nginx:1.15

ARG appname
ENV APP_NAME $appname

WORKDIR /${APP_NAME}
COPY deploy/nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /$APP_NAME/dist .

ENV POD_PORT "80"

CMD ["sh", "-c", "nginx -g 'daemon off;'"]
