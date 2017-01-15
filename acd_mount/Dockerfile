FROM python:3.5

MAINTAINER Michael Baudino <michael.baudino@alpine-lab.com>

# Install required packages
RUN apt-get update \
 && apt-get install -y --no-install-recommends --no-install-suggests \
      fuse \
      libfuse2 \
      encfs \
      unionfs-fuse \
      build-essential

# Install acd_cli
RUN pip install --upgrade git+https://github.com/yadayada/acd_cli.git

# Install fswatch
RUN cd /usr/local/src \
 && wget https://github.com/emcrisostomo/fswatch/releases/download/1.9.3/fswatch-1.9.3.tar.gz \
 && pwd \
 && find . \
 && tar xvzf fswatch-1.9.3.tar.gz \
 && cd fswatch-1.9.3 \
 && ./configure && make && make check && make install \
# && make distclean \
# && rm -rf /usr/local/src/fswatch

# Cleanup
RUN apt-get --purge -y remove build-essential \
 && apt-get --purge -y autoremove \
 && apt-get -y clean autoclean \
 && rm -rf /var/lib/apt/lists/*

# Install custom scripts
COPY bin/* /usr/local/bin/

# Declare default command
CMD ["acd_mount"]
