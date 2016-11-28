FROM kamehouse/nginx:latest

MAINTAINER Michael Baudino <mike@kamehou.se>

# install required packages
RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
          transmission-daemon
    && rm -rf /var/lib/apt/lists/*

COPY transmission /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/transmssion /etc/nginx/sites-enabled/
