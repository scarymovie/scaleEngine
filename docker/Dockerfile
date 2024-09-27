FROM alpine:3.20

RUN apk add nginx

COPY ./public /usr/share/nginx/html

ENTRYPOINT ["top", "-b"]