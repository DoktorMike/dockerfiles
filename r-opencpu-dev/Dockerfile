# Look here for details: https://hub.docker.com/r/opencpu/base/
FROM opencpu/base

MAINTAINER Michael Green micke.green@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# Install development tools
RUN apt-get update \
        && apt-get install -y --no-install-recommends \
        rstudio-server \
        r-base-dev \
        sudo \
        curl \
        git \
        libcurl4-openssl-dev \
        libssl-dev \
        libxml2-dev \
        libssh2-1-dev \
        libgdal-dev \
        libudunits2-dev

RUN R -e "require(remotes); remotes::install_github('DoktorMike/datools')"

RUN R -e "install.packages(c('brms', 'ggmcmc', 'bayesplot'))"

# Workaround for rstudio apparmor bug
RUN echo "server-app-armor-enabled=0" >> /etc/rstudio/rserver.conf

# Cleanup
RUN cd / \
  && rm -rf /tmp/* \
  && apt-get autoremove -y \
  && apt-get autoclean -y \
  && rm -rf /var/lib/apt/lists/*

CMD service cron start && /usr/lib/rstudio-server/bin/rserver && apachectl -DFOREGROUND
