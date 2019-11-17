FROM alpine:latest

RUN apk add --no-cache curl && \
    mkdir -p /kettu && \
    curl -L https://github.com/endor/kettu/archive/master.tar.gz \
    | tar xz -C /kettu --strip-components=1 && \
    apk del --rdepends curl

ARG _VERSION=2.94-r2

RUN apk add --no-cache transmission-daemon=$_VERSION

EXPOSE 9091 51413
VOLUME ["/config", "/media", "/downloads"]

USER 1000:1000
CMD ["transmission-daemon", "--foreground", "--config-dir", "/config", "--no-watch-dir", "--no-incomplete-dir"]