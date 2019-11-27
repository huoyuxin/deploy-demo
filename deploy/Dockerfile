FROM jelastic/nodejs:10.16.3-forever

WORKDIR /data/server

COPY package.json package-lock.json ./
# install deps
# RUN npm set strict-ssl false
RUN npm install

# build
COPY . ./
RUN npm run build

FROM nginx:1.15

WORKDIR /data/server
COPY deploy/nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /dist .

ENV POD_PORT "80"

CMD ["sh", "-c", "/etc/nginx/nginx.conf \
     && nginx -g 'daemon off;'"]
