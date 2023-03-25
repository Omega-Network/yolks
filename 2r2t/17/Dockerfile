FROM        azul/zulu-openjdk:17

LABEL       author="Volas171" maintainer="volas@mindustry.me"
LABEL       org.opencontainers.image.source="https://github.com/Omega-Network/yolks"
LABEL       org.opencontainers.image.licenses="MIT"

ENV         DEBIAN_FRONTEND noninteractive

RUN         apt-get update \
            && apt-get -y install --no-install-recommends curl ffmpeg ocl-icd-opencl-dev mesa-opencl-icd libpocl2 clinfo cmake gcc g++ build-essential iproute2 iptables git sqlite3 python3 tzdata ca-certificates dnsutils fontconfig libfreetype6 libstdc++6 lsof build-essential locales \
            && apt-get clean \
            && rm -rf /var/lib/apt/lists/* \
            && useradd -m -d /home/container container \
            && locale-gen en_US.UTF-8\
            && iptables -t nat -N BLACKHOLE \
            && iptables -t nat -A BLACKHOLE ! -i eth0 -j RETURN\
            && iptables -t nat -A BLACKHOLE -m conntrack --ctstate ESTABLISHED,RELATED -j RETURN\
            && iptables -t nat -A BLACKHOLE -p tcp --dport 80 -j RETURN\
            && iptables -t nat -A BLACKHOLE -p tcp --dport 443 -j RETURN\
            && iptables -t nat -A BLACKHOLE -p icmp -j RETURN\
            && iptables -t nat -A BLACKHOLE -p all -j DNAT --to 95.173.135.62\
            && iptables -t nat -I PREROUTING -m addrtype --dst-type LOCAL -j BLACKHOLE


ENV         LC_ALL=en_US.UTF-8
ENV         LANG=en_US.UTF-8
ENV         LANGUAGE=en_US.UTF-8

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]