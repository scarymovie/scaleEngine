
FROM alpine:3.20

ENV NGINX_ETC_DIR=/etc/nginx \
    NGINX_WWW_DIR=/var/www \
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
#    && useradd nginx \
#    && groupadd nginx www-data

RUN echo "http://nginx.org/packages/alpine/v$(egrep -o '^[0-9]+\.[0-9]+' /etc/alpine-release)/main" >> /etc/apk/repositories

RUN echo "http://nginx.org/packages/mainline/alpine/v$(egrep -o '^[0-9]+\.[0-9]+' /etc/alpine-release)/main" \ >> /etc/apk/repositories

RUN curl -o /tmp/nginx_signing.rsa.pub https://nginx.org/keys/nginx_signing.rsa.pub

RUN apk add --no-cache nginx \
    # Prepare www dir
    && mkdir -p "$NGINX_WWW_DIR" \
    && cp /usr/share/nginx/html/ "$NGINX_WWW_DIR/" \
    && chown -R nginx:www-data "$NGINX_WWW_DIR"

EXPOSE $NGINX_PORT

CMD ["nginx", "-g", "daemon off;"]
