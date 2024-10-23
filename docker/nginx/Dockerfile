
FROM alpine:3.20

ENV NGINX_ETC_DIR=/etc/nginx \
    NGINX_WWW_DIR=/var/www/public \
    NGINX_PORT=8080

COPY nginx.conf $NGINX_ETC_DIR/nginx.conf
COPY index.html $NGINX_WWW_DIR/index.html

RUN set -ex \
    && apk update \
    && apk add --no-cache \
        openssl \
        curl \
        ca-certificates \
    && update-ca-certificates \
    && addgroup -S www-data || true \
    && adduser -S -G www-data nginx \
    && curl -o /tmp/nginx_signing.rsa.pub https://nginx.org/keys/nginx_signing.rsa.pub \
    && apk add --no-cache nginx \
    && mkdir -p "$NGINX_WWW_DIR" \
    && chown -R nginx:www-data "$NGINX_WWW_DIR" \
    && rm -rf /var/cache/apk/*

EXPOSE $NGINX_PORT

CMD ["nginx", "-g", "daemon off;"]
