ARG ALPINE_VERSION

FROM alpine:${ALPINE_VERSION}

ARG TZ

RUN apk update \
    && apk upgrade \
    && apk add --no-cache bash \
    && apk add --no-cache tzdata \
    && cp /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone

WORKDIR /srv/docker-alpine

COPY ./cron/example.sh ./cron/example.sh
RUN chmod 755 /srv/docker-alpine/cron/example.sh

COPY ./docker-entrypoint.sh .
RUN chmod 755 /srv/docker-alpine/docker-entrypoint.sh

RUN apk add --no-cache bash

ENTRYPOINT ["/srv/docker-alpine/docker-entrypoint.sh"]
