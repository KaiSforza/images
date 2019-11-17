FROM mono:latest

ARG DEBIAN_FRONTEND="noninteractive"
ENV XDG_DATA_HOME="/config" \
    XDG_CONFIG_HOME="/config"

RUN apt-get update
RUN apt-get install -y --no-install-recommends curl libmediainfo0v5

ARG _VERSION=1

RUN mkdir -p /Sonarr && \
    echo "Downloading version $_VERSION" && \
    curl -kL "https://download.sonarr.tv/v3/phantom-develop/${_VERSION}/Sonarr.phantom-develop.${_VERSION}.linux.tar.gz" \
    | tar -xz -C /Sonarr --strip-components=1
RUN apt-get autoremove -y curl && apt-get clean

RUN mkdir -pv /Sonarr /config /downloads && \
    chown -R 1000:1000 /Sonarr /config /downloads

RUN rm -rf /var/lib/apt/lists/*

VOLUME /config /downloads
EXPOSE 8989

USER 1000:1000
CMD ["mono", "--debug", "/Sonarr/Sonarr.exe", "-nobrowser", "-data=/config"]