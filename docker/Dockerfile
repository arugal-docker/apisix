FROM api7/apisix-base:dev AS build

ARG ENABLE_PROXY=false

ENV DEBIAN_FRONTEND noninteractive

COPY . /apisix
WORKDIR /apisix

RUN set -x \
    && (test "${ENABLE_PROXY}" != "true" || /bin/sed -i 's,http://deb.debian.org,http://mirrors.aliyun.com,g' /etc/apt/sources.list) \
    && apt-get -y update --fix-missing \
    && apt-get install -y curl \
        gawk \
        git \
        libldap2-dev \
        liblua5.1-0-dev \
        lua5.1 \
        make \
        sudo \
        unzip \
        wget \
        gnupg2

RUN set -x \
    && bash utils/install-dependencies.sh \
    && make deps \
    && make install
