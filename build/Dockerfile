FROM debian:bullseye-slim as build

ARG MONERO_VERSION=v0.17.1.9
ENV FILENAME monero-linux-x64-${MONERO_VERSION}.tar.bz2
ENV DOWNLOAD_URL https://downloads.getmonero.org/cli/${FILENAME}

ADD $DOWNLOAD_URL /$FILENAME
RUN apt-get update -y;\
    apt-get install bzip2 -y;\
    tar --strip-components=1 -C /usr/bin -jxvf  /$FILENAME;
    
FROM debian:bullseye-slim

EXPOSE 18081
EXPOSE 18080

COPY --from=build /usr/bin/monerod /usr/bin/monerod

ENTRYPOINT monerod --p2p-bind-ip=0.0.0.0 --p2p-bind-port=18080 --rpc-bind-ip=0.0.0.0 --rpc-bind-port=18081 --non-interactive --confirm-external-bind $EXTRA_OPTS
