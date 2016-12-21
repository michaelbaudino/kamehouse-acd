FROM python:3.5

MAINTAINER Michael Baudino <michael.baudino@alpine-lab.com>

RUN apt-get update \
 && apt-get install -y --no-install-recommends --no-install-suggests \
      fuse \
      libfuse2 \
 && pip install --upgrade git+https://github.com/yadayada/acd_cli.git

COPY bin/* /usr/local/bin/

CMD ["acd_mount"]
