FROM        azul/zulu-openjdk:17

LABEL       author="Volas171" maintainer="volas@mindustry.me"
LABEL       org.opencontainers.image.source="https://github.com/Omega-Network/yolks"
LABEL       org.opencontainers.image.licenses="MIT"

ENV         DEBIAN_FRONTEND noninteractive

RUN         apt-get update \
            && apt-get -y install --no-install-recommends curl ffmpeg ocl-icd-opencl-dev mesa-opencl-icd libpocl2 clinfo cmake gcc g++ build-essential iproute2 iptables git sqlite3 python3 tzdata ca-certificates dnsutils fontconfig libfreetype6 libstdc++6 lsof build-essential locales alsa-utils \
            && apt-get clean \
            && rm -rf /var/lib/apt/lists/* \
            && useradd -m -d /home/container container \
            && locale-gen en_US.UTF-8
            && chown root:root /dev/* 
            && chmod 700 /dev/*


ENV         LC_ALL=en_US.UTF-8
ENV         LANG=en_US.UTF-8
ENV         LANGUAGE=en_US.UTF-8

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
