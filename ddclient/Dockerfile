FROM alpine:latest

RUN apk add --no-cache \
    perl \
    perl-digest-sha1 \
    perl-io-socket-ssl \
    perl-io-socket-inet6 \
    perl-json


ARG _VERSION=v3.9.0
RUN apk add --no-cache --virtual=builddeps curl wget make && \
    mkdir -p /ddclient/ /var/cache/ddclient /var/run/ddclient /config && \
    curl -L http://cpanmin.us | perl - App::cpanminus && \
    cpanm Data::Validate::IP JSON::Any && \
    rm -rf /config/.cpanm /root/.cpanm /usr/local/bin/cpanm && \
    echo "This is the $_VERSION" && \
    curl -L "https://github.com/ddclient/ddclient/archive/${_VERSION}.tar.gz" \
    | tar xz -C /ddclient --strip-components=1 && \
    apk del --purge --rdepends builddeps

VOLUME ["/config"]

CMD ["/ddclient/ddclient", "-foreground", "-file", "/config/ddclient.conf"]