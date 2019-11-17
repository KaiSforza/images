FROM ubuntu:18.04

ARG DEBIAN_FRONTEND="noninteractive"
ENV XDG_DATA_HOME="/config" \
XDG_CONFIG_HOME="/config"

RUN apt-get update
RUN apt-get install -y --no-install-recommends libicu60 libssl1.0 ca-certificates curl

ARG _VERSION=1

RUN mkdir -p /Jackett && \
    curl -kL "https://github.com/Jackett/Jackett/releases/download/${_VERSION}/Jackett.Binaries.LinuxAMDx64.tar.gz" \
    | tar -xz -C /Jackett --strip-components=1
RUN apt-get autoremove -y curl && apt-get clean

RUN mkdir -pv /jackett /config /downloads && \
    chown -R 1000:1000 /jackett /config /downloads

RUN rm -rf /var/lib/apt/lists/*

VOLUME /config /downloads
EXPOSE 9117

USER 1000:1000
CMD ["/Jackett/jackett", "--NoRestart"]