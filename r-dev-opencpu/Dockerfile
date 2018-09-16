# Look here for details: https://hub.docker.com/r/opencpu/base/
FROM opencpu/base

MAINTAINER Michael Green micke.green@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# Install.
RUN \
  apt-get update && \
  apt-get -y dist-upgrade && \
  apt-get install -y software-properties-common && \
  add-apt-repository -y ppa:marutter/rrutter && \
  apt-get update && \
  apt-get install -y wget make devscripts apache2-dev apache2 libapreq2-dev \
                     r-base r-base-dev libapparmor-dev libcurl4-openssl-dev \
                     libprotobuf-dev protobuf-compiler xvfb xauth xfonts-base curl \
                     libssl-dev libxml2-dev libicu-dev pkg-config libssh2-1-dev \
                     locales apt-utils && \
  useradd -ms /bin/bash builder

