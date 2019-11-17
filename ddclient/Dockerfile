FROM alpine:latest

RUN apk add --no-cache \
    perl \
    perl-digest-sha1 \
    perl-io-socket-ssl \
    perl-io-socket-inet6 \
    perl-json


RUN apk add --no-cache --virtual=builddeps curl wget make
RUN mkdir -p /ddclient/ /var/cache/ddclient /var/run/ddclient /config

RUN curl -L http://cpanmin.us | perl - App::cpanminus && \
    cpanm Data::Validate::IP JSON::Any && \
    rm -rf /config/.cpanm /root/.cpanm /usr/local/bin/cpanm

ARG _VERSION=v3.9.0

RUN echo "This is the $_VERSION" && \
    curl -L "https://github.com/ddclient/ddclient/archive/${_VERSION}.tar.gz" \
    | tar xz -C /ddclient --strip-components=1

RUN apk del --purge --rdepends builddeps

VOLUME ["/config"]

CMD ["/ddclient/ddclient", "-foreground", "-file", "/config/ddclient.conf"]