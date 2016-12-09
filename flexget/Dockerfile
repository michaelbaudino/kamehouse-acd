FROM python:3.5

RUN pip install -I flexget transmissionrpc

RUN mkdir -p /flexget
COPY config.template.yml /flexget/config.template.yml

WORKDIR /flexget

COPY flexget-config-replacer /usr/local/bin

ENTRYPOINT ["flexget-config-replacer"]
CMD ["flexget", "--loglevel", "verbose", "-c", "/flexget/config.yml", "daemon", "start"]
