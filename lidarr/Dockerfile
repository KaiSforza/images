FROM mono:latest

ARG DEBIAN_FRONTEND="noninteractive"
ENV XDG_DATA_HOME="/config" \
    XDG_CONFIG_HOME="/config"

RUN apt-get update
RUN apt-get install -y --no-install-recommends sqlite libchromaprint1

ARG _VERSION=1

RUN mkdir -p /Lidarr && \
    echo "Downloading version $_VERSION" && \
    curl -kL "https://github.com/lidarr/Lidarr/releases/download/v${_VERSION}/Lidarr.master.${_VERSION}.linux.tar.gz" \
    | tar -xz -C /Lidarr --strip-components=1
RUN apt-get autoremove -y curl && apt-get clean

RUN mkdir -pv /Lidarr /config /downloads && \
    chown -R 1000:1000 /Lidarr /config /downloads

RUN rm -rf /var/lib/apt/lists/*

VOLUME /config /downloads
EXPOSE 7878

USER 1000:1000
CMD ["mono", "--debug", "/Lidarr/Lidarr.exe", "-nobrowser", "-data=/config"]