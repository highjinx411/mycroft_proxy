FROM nginx

#  default conf for proxy service
COPY ../nginx/default.conf /etc/nginx/conf.d/default.conf


# Proxy SSL certificates
COPY ./ssl/ /etc/ssl/certs/nginx/
