FROM mono:latest

ARG DEBIAN_FRONTEND="noninteractive"
ENV XDG_DATA_HOME="/config" \
    XDG_CONFIG_HOME="/config"

RUN apt-get update
RUN apt-get install -y --no-install-recommends curl libmediainfo0v5

ARG _VERSION=1

RUN mkdir -p /Radarr && \
    echo "Downloading version $_VERSION" && \
    curl -kL "https://github.com/Radarr/Radarr/releases/download/v${_VERSION}/Radarr.develop.${_VERSION}.linux.tar.gz" \
    | tar -xz -C /Radarr --strip-components=1
RUN apt-get autoremove -y curl && apt-get clean

RUN mkdir -pv /Radarr /config /downloads && \
    chown -R 1000:1000 /Radarr /config /downloads

RUN rm -rf /var/lib/apt/lists/*

VOLUME /config /downloads
EXPOSE 7878

USER 1000:1000
CMD ["mono", "--debug", "/Radarr/Radarr.exe", "-nobrowser", "-data=/config"]