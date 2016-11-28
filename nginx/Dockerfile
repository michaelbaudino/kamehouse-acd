FROM ubuntu:16.04

MAINTAINER Michael Baudino <mike@kamehou.se>

# install required packages
RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
          nginx \
          letsencrypt \
    && rm -rf /var/lib/apt/lists/*

# remove default nginx config
RUN rm -f /etc/nginx/sites-enabled/default

# add an nginx config that redirects all HTTP traffic to HTTPS
COPY force_https /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/force_https /etc/nginx/sites-enabled/

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

# copy letsencrypt-related scripts
COPY setup renew-letsencrypt-certs /usr/local/bin/

# expose HTTP(S) ports
EXPOSE 80 443

# start nginx
CMD ["nginx", "-g", "daemon off;"]
