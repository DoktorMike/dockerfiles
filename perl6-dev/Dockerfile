FROM buildpack-deps:xenial-curl
MAINTAINER "Michael Green" micke.green@gmail.com

RUN groupadd -r perl6 && useradd -r -g perl6 perl6
RUN useradd docker && mkdir /home/docker && chown docker:docker /home/docker && addgroup docker staff

# procps is very common in build systems, and is a reasonably small package
RUN apt-get update && apt-get install -y --no-install-recommends \
		bzr \
		git \
		mercurial \
		openssh-client \
		subversion \
		\
		procps \
	&& rm -rf /var/lib/apt/lists/*

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		software-properties-common ed less locales vim-tiny wget \
		ca-certificates libcurl4-openssl-dev libssl-dev \
  && add-apt-repository --enable-source --yes "ppa:marutter/rrutter" \
	&& add-apt-repository --enable-source --yes "ppa:marutter/c2d4u"

## Configure default locale, see https://github.com/rocker-org/rocker/issues/19
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen en_US.utf8 && /usr/sbin/update-locale LANG=en_US.UTF-8

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV rakudo_version=2017.04

RUN buildDeps=' \
        gcc \
        libc6-dev \
        libencode-perl \
        make \
    ' \
    && set -x \
    && apt-get update \
    && apt-get --yes install --no-install-recommends $buildDeps \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir /root/rakudo \
    && curl -fsSL http://rakudo.org/downloads/star/rakudo-star-${rakudo_version}.tar.gz -o rakudo.tar.gz \
    && tar xzf rakudo.tar.gz --strip-components=1 -C /root/rakudo \
    && ( \
        cd /root/rakudo \
        && perl Configure.pl --prefix=/usr --gen-moar \
        && make install \
    ) \
    && rm -rf /rakudo.tar.gz /root/rakudo \
    && apt-get purge -y --auto-remove $buildDeps

ENV PATH=$PATH:/usr/share/perl6/site/bin
