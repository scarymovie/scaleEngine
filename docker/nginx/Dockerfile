FROM alpine:3.20.3

RUN apk add --no-cache openssl curl ca-certificates

RUN echo "http://nginx.org/packages/alpine/v$(egrep -o '^[0-9]+\.[0-9]+' /etc/alpine-release)/main" >> /etc/apk/repositories

RUN echo "http://nginx.org/packages/mainline/alpine/v$(egrep -o '^[0-9]+\.[0-9]+' /etc/alpine-release)/main" \ >> /etc/apk/repositories

RUN curl -o /tmp/nginx_signing.rsa.pub https://nginx.org/keys/nginx_signing.rsa.pub

RUN apk add --no-cache nginx

COPY nginx.conf /etc/nginx/nginx.conf
COPY index.html /var/www/html/index.html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
