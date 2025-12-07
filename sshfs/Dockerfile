ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base/amd64:6.2.7
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base system
ARG BUILD_ARCH=amd64
ARG INFLUXDB_VERSION="2.7.1"
ARG INFLUXCLI_VERSION="2.7.3"
ARG TRAEFIK_VERSION="2.10.4"

RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        luarocks=2.4.2+dfsg-1.1 \
        procps=2:3.3.17-5 \
        sshfs \
    \
    && ARCH="${BUILD_ARCH}" \
    && if [ "${BUILD_ARCH}" = "aarch64" ]; then ARCH="arm64"; fi \
    && if [ "${BUILD_ARCH}" = "armv7" ]; then ARCH="armhf"; fi 

# Copy root filesystem
COPY rootfs /


# Copy data for add-on
RUN chmod a+x /usr/bin/run.sh

CMD [ "run.sh" ]
