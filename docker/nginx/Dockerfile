FROM alpine:3.20

ENV NGINX_ETC_DIR=/etc/nginx \
    NGINX_WWW_DIR=/var/www/public \
    NGINX_PORT=8081 \
    ENTRYPOINT_DIR=/usr/local/bin \
    CERTS_DIR=/etc/nginx/ssl

COPY nginx.conf $NGINX_ETC_DIR/nginx.conf
COPY index.html $NGINX_WWW_DIR/index.html
COPY entrypoint.sh $ENTRYPOINT_DIR/entrypoint.sh

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
    && mkdir -p $CERTS_DIR \
    && openssl req -x509 -out $CERTS_DIR/localhost.crt -keyout $CERTS_DIR/localhost.key \
         -newkey rsa:2048 -nodes -sha256 \
         -subj '/CN=localhost' -extensions EXT -config <( \
          printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth") \
    && chmod 600 $CERTS_DIR/localhost.* \
    && update-ca-certificates \
    && chown -R nginx:www-data "$NGINX_WWW_DIR" \
    && rm -rf /var/cache/apk/* \
    && chmod +x $ENTRYPOINT_DIR/entrypoint.sh

EXPOSE $NGINX_PORT 443

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]