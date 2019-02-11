ARG REDIS_VERSION=alpine

FROM redis:${REDIS_VERSION}

LABEL maintainer="Angel Aviel Domaoan <tenshiAMD@users.noreply.github.com>"

ENV REDIS_HOME /var/lib/redis
ENV REDIS_PORT 6379
ENV REDIS_USER redis

USER root

RUN mkdir $REDIS_HOME && chown -R $REDIS_USER:$REDIS_USER $REDIS_HOME

VOLUME $REDIS_HOME
WORKDIR $REDIS_HOME

COPY redis.conf /usr/local/etc/redis/redis.conf

CMD ["redis-server", "/usr/local/etc/redis/redis.conf"]

COPY docker-healthcheck.sh /usr/local/bin/docker-healthcheck.sh
RUN cd /usr/local/bin && chmod 750 docker-healthcheck.sh
RUN chown $REDIS_USER:$REDIS_USER /usr/local/bin/docker-healthcheck.sh

HEALTHCHECK CMD ["docker-healthcheck.sh"]

USER $REDIS_USER

EXPOSE $REDIS_PORT
