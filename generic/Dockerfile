ARG BUILD_FROM
FROM ${BUILD_FROM}:3.0

WORKDIR /usr/src
ARG BUILD_VERSION

## Setup Home Assistant
# hadolint ignore=DL3013
RUN git clone --depth 1 --branch "${BUILD_VERSION}" https://github.com/home-assistant/home-assistant homeassistant \
    && rm -rf homeassistant/.git \
    && pip3 install --no-cache-dir --no-index --only-binary=:all: --find-links "${WHEELS_LINKS}" \
        -r homeassistant/requirements_all.txt -c homeassistant/homeassistant/package_constraints.txt \
    && pip3 install --no-cache-dir --no-index --only-binary=:all: --find-links "${WHEELS_LINKS}" \
        -e ./homeassistant \
    && python3 -m compileall homeassistant/homeassistant

# Run Home Assistant
WORKDIR /config
CMD [ "python3", "-m", "homeassistant", "--config", "/config" ]
