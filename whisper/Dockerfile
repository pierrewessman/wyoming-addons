# HOWTO: docker run -it --rm --gpus '"device=0"' .
FROM nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04

# Install Whisper
WORKDIR /usr/src
ARG WYOMING_WHISPER_VERSION='2.1.0'

RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        python3 \
        python3-dev \
        python3-pip \
    \
    && pip3 install --no-cache-dir -U \
        setuptools \
        wheel \
    && pip3 install --no-cache-dir \
        --extra-index-url https://www.piwheels.org/simple \
        "wyoming-faster-whisper @ https://github.com/rhasspy/wyoming-faster-whisper/archive/refs/tags/v${WYOMING_WHISPER_VERSION}.tar.gz" \
    \
    && apt-get purge -y --auto-remove \
        build-essential \
        python3-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /
COPY run.sh ./

ENV LD_LIBRARY_PATH /usr/lib/x86_64-linux-gnu
EXPOSE 10300

ENTRYPOINT ["bash", "/run.sh"]
