FROM nginx:alpine

RUN mkdir -p /var/www/public

COPY nginx.conf /etc/nginx/nginx.conf
COPY index.html /var/www/public

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
