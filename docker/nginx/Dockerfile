FROM alpine:3.20.3

RUN apk add --no-cache nginx

RUN mkdir -p /var/www/public

COPY nginx.conf /etc/nginx/nginx.conf
COPY index.html /var/www/public

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
