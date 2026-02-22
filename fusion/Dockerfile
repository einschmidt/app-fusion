ARG BUILD_FROM
# hadolint ignore=DL3006
FROM $BUILD_FROM

# Use bash as the default shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# https://github.com/0x2E/fusion/releases
ARG FUSION_VERSION="v1.1.0"

# Install lldap
ARG BUILD_ARCH=amd64
RUN \
    set -eux \
    \
    && if [[ "$BUILD_ARCH" = "aarch64" ]]; then ARCH="arm64"; fi \
    && if [[ "$BUILD_ARCH" = "amd64" ]]; then ARCH="amd64"; fi \
    \
    && curl -J -L -o /tmp/fusion.zip "https://github.com/0x2E/fusion/releases/download/${FUSION_VERSION}/fusion_linux_${ARCH}.zip" \
    && unzip /tmp/fusion.zip -d /usr/local/bin/ \
    \
    && chmod -R +x /usr/local/bin/fusion \
    \
    && rm -rf /tmp/*

# Copy root filesystem
COPY rootfs /

# Set environment variables
ENV PORT=7080
ENV DB="/data/fusion.db"

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Einschmidt" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Einschmidt" \
    org.opencontainers.image.authors="einschmidt" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://google.com" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}